# Introduction

This repository contains code for the AER continuum used in [LBLRTM](https://github.com/AER-RC/LBLRTM) and as a standalone model, MT_CKD. MT_CKD is an enhancement ot the original CKD model

# Cloning the Latest Release

Assuming the output directory should be `mt-ckd`:

`git clone --recursive git@github.com:AER-RC/mt-ckd.git`

`--recursive` is important, because this repository is linked with our [common FORTRAN modules repository](https://github.com/AER-RC/aer_rt_utils) that are required in the model builds. Because [LBLRTM](https://github.com/AER-RC/LBLRTM) uses the continuum, it, too, is also added as a submodule and a couple of its source files link to the LBLRTM submodule (`contnm.f90`, `lblparams.f90`, `phys_consts.f90`, and `planet_earth.f90`). If this keyword is forgotten, one can do:

```
git submodule init
git submodule update
```

in the `mt-ckd` directory.

Currently, the latest release is MT_CKD v3.3, and it is recommended that this be the version that users clone and checkout (rather than the `master` branch). To do this, one needs to simply checkout the `v3.3` tag:

```
git checkout tags/v3.3
```

# Building

To build the continuum model:

```
cd mt-ckd/build
make -f make_cntnm $TARGET
```

The `TARGET` environment variable depends on the user's operating system, compiler, and desired precision. Available targets are:

| Target | Description | Compiler |
| :--- | :--- | :--- |
| `aixIBMsgl` | IBM/AIX OS using IBM fortran,single precision| `xlf90` |
| `linuxPGIsgl` | Linux OS using PGI fortran,single precision |  `pgf90` |
| `linuxGNUsgl` | Linux OS using GNU fortran,single precision | `gfortran` |
| `linuxG95sgl` | Linux OS using G95 fortran,single precision | `g95` |
| `inuxINTELsgl` | Linux OS using Intel fortran,single precision | `ifort` |
| `mingwGNUsgl` | Windows unix shell environment using gfortran,single precision | `gfortran` |
| `osxABSOFTsgl` | Mac OS_X using Absoft Pro fortran,singleprecision | `f90` |
| `osxGNUsgl` | Mac OS_X using GNU fortran,singleprecision | `gfortran` |
| `osxIBMsgl` | Mac OS_X using IBM XL fortran,singleprecision | `xlf90` |
| `osxINTELsgl` | Mac OS_X using Intel fortran,single precision | `ifort` |
| `sunSUNsgl` | Sun/Solaris OS using Sun fortran,single precision | `sunf90` |
| `sgiMIPSsgl` | SGI/IRIX64 OS using MIPS fortran,single precision | `f90` |

# Run Example

To run MT_CKD as a standalone program instead of in LBLRTM:

```
cd run_example/
ln -s ../cntnm_v3.3_linux_pgi_dbl cntnm # assuming v3.3 was built with PGI in double precision (linuxPGIdbl)
./cntnm (0, enter)
```

Push 0, then enter, and `CNTNM.OPTDPT` and `WATER.COEF` will be written to working directory. These can be compared with `CNTNM.OPTDPT_mt_ckd_AER` and `WATER.COEF_mt_ckd_AER`, which are included in version control and are considered the baseline calculations. They change with every release and will be updated accordingly.

For other runs of the continuum standalone program, the user can edit `INPUT.example` in the `run_example` directory.
