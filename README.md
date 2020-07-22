# mt-ckd
AER continuum

`git clone --recursive git@github.com:AER-RC/mt-ckd.git`

# Building

```
cd mt-ckd/build
make -f make_cntnm linuxPGIdbl
```

# Run Example

```
cd run_example/
ln -s ../cntnm_v3.0_linux_pgi_dbl cntnm # assuming v3.0 was built with PGI in double precision (linuxPGIdbl)
./cntnm (0, enter)
```

Push 0, then enter, and `CNTNM.OPTDPT` and `WATER.COEF` will be written to working directory. These can be compared with `CNTNM.OPTDPT_mt_ckd_AER` and `WATER.COEF_mt_ckd_AER`, which are included in version control and are considered the baseline calculations. They change with every release and will be updated accordingly.
