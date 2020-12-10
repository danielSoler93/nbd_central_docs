.. NBD documentation master file, created by
   sphinx-quickstart on Mon Dec  4 11:58:09 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Tests
=========

Tests are runned every day at night at nbdcalc01 (officecomputer).
These tests install all python packages through conda and run the
examples/tests of the different packages. (As clients would do)

All tests are centralize and spawn from jenkins platform set locally
in the nbcalc01 machine. You can enter by:

   - connect to nbdcalc01
   - firefox 192.168.1.3:8080/jenkins &
   - ask to Nostrum Support for the user_name & password

Inside jenkins you will find the next projects with all their
bash instructions under project/configure


.. figure:: tests.png
    :scale: 100%
    :align: center

Test schedule
===============

Every day the deployment (installation & tests) of the next packages will be tested:

1) 1:00 am --> python packages (analgos_finder, modtox & miscellaneous packages)

2) 2:00 am --> frag_pele

3) 2:30 am --> adaptive_pele

4) 3:00 am --> msm_pele

3) 3:30 am --> PELE


