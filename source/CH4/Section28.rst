Softwares and Installation
==============================================================

Softwares
--------------------------------------------------------------

1. `User Guide to Semiempirical Tight Binding (xtb doc) <https://xtb-docs.readthedocs.io/en/latest/contents.html>`_
2. `ORCA tutorial (FAccTs) <https://www.orcasoftware.de/tutorials_orca/index.html>`_
3. `Avogadro Software <https://avogadro.cc/>`_
4. `Visual Molecular Dynamics (VMD) <https://www.ks.uiuc.edu/Research/vmd/>`_
5. `Jmol <http://jmol.sourceforge.net/>`_
6. `JANPA <http://janpa.sourceforge.net/>`_
7. `Molclus <http://www.keinsci.com/research/molclus.html>`_

Installation (censo)
---------------------------------------------------------------------

| 4 different projects (xtb, crest, censo and orca) are needed to install your system and, but unfortunately, crest and censo only run under on linux operating systems.
|
| OS version: UBUNTU 20.04, 22.04 and 24.04.
| Xtb version: 6.4.1
| Crest verison: 2.11.2
| Censo version: 1.2.0
| Orca version:  6.0.2 or 6.0.3 (need OipenMPI 4.1.1)

| Assigning PATH variables
| Below is added code in my .bashrc file

.. code-block:: bash

        #openmpi
        export PATH="$HOME/openmpi-4.1.1/bin:$PATH"; export LD_LIBRARY_PATH="$HOME/openmpi-4.1.1/lib:$LD_LIBRARY_PATH"
        
        #orca
        export PATH="$HOME/orca_5_0_2_linux_x86-64_shared_openmpi411:$PATH"; export LD_LIBRARY_PATH="$HOME/orca_5_0_2_linux_x86-64_shared_openmpi411:$LD_LIBRARY_PATH"

        #xtb
        export PATH=$PATH:/home/vitamin/xtb-6.4.1/bin
        export XTBPATH=/home/vitamin/xtb-6.4.1/share/xtb
        export OMP_NUM_THREADS=8
        export MKL_NUM_THREADS=8
        export OMP_STACKSIZE=3000m
        ulimit -s unlimited

| If your can not executive your program, you can symbolic link or copy to your .local/bin/

.. code-block:: bash
        
        cp anmr ~/.local/bin/

.. code-block:: bash

        ln -s ~/anmr ~/.local/bin/


This is my .censorc file setting (only for Hydrogen NMR and use revTPSS)
This program is fully automated computation of spin-spin NMR Spectra but sometimes the confermers can not converged to energy local minimum. The default of rthr, bthr and ethr are small and ewin is large, I write a bash to reduce the numbers of conformers.


.. code-block:: bash

 $CENSO global configuration file: .censorc
 $VERSION:1.2.0
 
 ORCA: /home/vitamin/orca_5_0_2_linux_x86-64_shared_openmpi411
 ORCA version: 5.02
 GFN-xTB: /home/vitamin/xtb-6.4.1/bin/xtb
 CREST: /home/vitamin/crest-binary-2.11.1/crest
 mpshift: /path/including/binary/mpshift-binary
 escf: /path/including/binary/escf-binary
 
 #COSMO-RS
 #ctd = BP_TZVP_C30_1601.ctd cdir = "/software/cluster/COSMOthermX16/COSMOtherm/CTDATA-FILES" ldir = "/software/cluster/COSMOthermX16/COSMOtherm/CTDATA-FILES"
 $ENDPROGRAMS
 
 $CRE SORTING SETTINGS:
 $GENERAL SETTINGS:
 nconf: all                       # ['all', 'number e.g. 10 up to all conformers'] 
 charge: 0                        # ['number e.g. 0'] 
 unpaired: 0                      # ['number e.g. 0'] 
 solvent: chcl3                     # ['gas', 'acetone', 'acetonitrile', 'aniline', 'benzaldehyde', 'benzene', 'ccl4', '...'] 
 prog_rrho: xtb                   # ['xtb'] 
 temperature: 298.15              # ['temperature in K e.g. 298.15'] 
 trange: [298.15, 298.15, 1]      # ['temperature range [start, end, step]'] 
 multitemp: off                   # ['on', 'off'] 
 evaluate_rrho: on                # ['on', 'off'] 
 consider_sym: on                 # ['on', 'off'] 
 bhess: on                        # ['on', 'off'] 
 imagthr: automatic               # ['automatic or e.g., -100    # in cm-1'] 
 sthr: automatic                  # ['automatic or e.g., 50     # in cm-1'] 
 scale: automatic                 # ['automatic or e.g., 1.0 '] 
 rmsdbias: off                    # ['on', 'off'] 
 sm_rrho: alpb                    # ['alpb', 'gbsa'] 
 progress: off                    # possibilities 
 check: on                        # ['on', 'off'] 
 prog: orca                       # ['tm', 'orca'] 
 func: r2scan-3c                  # ['b3-lyp', 'b3lyp', 'b3lyp-3c', 'b3lyp-d3', 'b3lyp-d3(0)', 'b3lyp-d4', 'b3lyp-nl', '...'] 
 basis: automatic                 # ['automatic', 'def2-TZVP', 'def2-mSVP', 'def2-mSVP', 'def2-mSVP', 'def2-mSVP', '...'] 
 maxthreads: 2                    # ['number of threads e.g. 2'] 
 omp: 4                           # ['number cores per thread e.g. 4'] 
 balance: on                      # possibilities 
 cosmorsparam: automatic          # ['automatic', '12-fine', '12-normal', '13-fine', '13-normal', '14-fine', '...'] 
 
 $PART0 - CHEAP-PRESCREENING - SETTINGS:
 part0: on                        # ['on', 'off'] 
 func0: r2scan-3c                 # ['b3-lyp', 'b3lyp', 'b3lyp-3c', 'b3lyp-d3', 'b3lyp-d3(0)', 'b3lyp-d4', '...'] 
 basis0: automatic                # ['automatic', 'def2-SV(P)', 'def2-TZVP', 'def2-mSVP', 'def2-mSVP', 'def2-mSVP', '...'] 
 part0_gfnv: gfn2                 # ['gfn1', 'gfn2', 'gfnff'] 
 part0_threshold: 4.0             # ['number e.g. 4.0'] 
 
 $PART1 - PRESCREENING - SETTINGS:
 # func and basis is set under GENERAL SETTINGS
 part1: on                        # ['on', 'off'] 
 smgsolv1: smd                    # ['alpb_gsolv', 'cosmo', 'cosmors', 'cosmors-fine', 'cpcm', 'dcosmors', '...'] 
 part1_gfnv: gfn2                 # ['gfn1', 'gfn2', 'gfnff'] 
 part1_threshold: 6               # ['number e.g. 5.0'] 
 
 $PART2 - OPTIMIZATION - SETTINGS:
 # func and basis is set under GENERAL SETTINGS
 part2: off                       # ['on', 'off'] 
 opt_limit: 4.0                   # ['number e.g. 4.0'] 
 sm2: cpcm                        # ['cosmo', 'cpcm', 'dcosmors', 'default', 'smd'] 
 smgsolv2: cpcm                   # ['alpb_gsolv', 'cosmo', 'cosmors', 'cosmors-fine', 'cpcm', 'dcosmors', '...'] 
 part2_gfnv: gfn2                 # ['gfn1', 'gfn2', 'gfnff'] 
 ancopt: on                       # ['on'] 
 hlow: 0.01                       # ['lowest force constant in ANC generation, e.g. 0.01'] 
 opt_spearman: off                # ['on', 'off'] 
 part2_threshold: 90              # ['Boltzmann sum threshold in %. e.g. 95 (between 1 and 100)'] 
 optlevel2: normal                # ['crude', 'sloppy', 'loose', 'lax', 'normal', 'tight', 'vtight', 'extreme', '...'] 
 optcycles: 4                     # ['number e.g. 5 or 10'] 
 spearmanthr: -4.0                # ['value between -1 and 1, if outside set automatically'] 
 radsize: 10                      # ['number e.g. 8 or 10'] 
 crestcheck: off                  # ['on', 'off'] 
 
 $PART3 - REFINEMENT - SETTINGS:
 part3: off                       # ['on', 'off'] 
 prog3: orca                      # ['tm', 'orca', 'prog'] 
 func3: pw6b95                    # ['b3-lyp', 'b3lyp', 'b3lyp-3c', 'b3lyp-d3', 'b3lyp-d3(0)', 'b3lyp-d4', 'b3lyp-nl', '...'] 
 basis3: def2-TZVPP               # ['DZ', 'QZV', 'QZVP', 'QZVPP', 'SV(P)', 'SVP', 'TZVP', 'TZVPP', 'aug-cc-pV5Z', '...'] 
 smgsolv3: cpcm                   # ['alpb_gsolv', 'cosmo', 'cosmors', 'cosmors-fine', 'cpcm', 'dcosmors', '...'] 
 part3_gfnv: gfn2                 # ['gfn1', 'gfn2', 'gfnff'] 
 part3_threshold: 95              # ['Boltzmann sum threshold in %. e.g. 95 (between 1 and 100)'] 
 
 $NMR PROPERTY SETTINGS:
 $PART4 SETTINGS:
 part4: on                        # ['on', 'off'] 
 couplings: on                    # ['on', 'off'] 
 progJ: orca                      # ['tm', 'orca', 'adf', 'prog'] 
 funcJ: pbe0                      # ['b3-lyp', 'b3lyp', 'b3lyp-3c', 'b3lyp-d3', 'b3lyp-d3(0)', 'b3lyp-d4', 'b3lyp-nl', '...'] 
 basisJ: pcJ-0                    # ['DZ', 'QZV', 'QZVP', 'QZVPP', 'SV(P)', 'SVP', 'TZVP', 'TZVPP', 'aug-cc-pV5Z', '...'] 
 sm4J: cpcm                       # ['cosmo', 'cpcm', 'dcosmors', 'smd'] 
 shieldings: on                   # ['on', 'off'] 
 progS: orca                      # ['tm', 'orca', 'adf', 'prog'] 
 funcS: revTPSS                   # ['b3-lyp', 'b3lyp', 'b3lyp-3c', 'b3lyp-d3', 'b3lyp-d3(0)', 'b3lyp-d4', 'b3lyp-nl', '...'] 
 basisS: pcSseg-1                 # ['DZ', 'QZV', 'QZVP', 'QZVPP', 'SV(P)', 'SVP', 'TZVP', 'TZVPP', 'aug-cc-pV5Z', '...'] 
 sm4S: cpcm                       # ['cosmo', 'cpcm', 'dcosmors', 'smd'] 
 reference_1H: TMS                # ['TMS'] 
 reference_13C: TMS               # ['TMS'] 
 reference_19F: CFCl3             # ['CFCl3'] 
 reference_29Si: TMS              # ['TMS'] 
 reference_31P: TMP               # ['TMP', 'PH3'] 
 1H_active: on                    # ['on', 'off'] 
 13C_active: off                  # ['on', 'off'] 
 19F_active: off                  # ['on', 'off'] 
 29Si_active: off                 # ['on', 'off'] 
 31P_active: off                  # ['on', 'off'] 
 resonance_frequency: 500.0       # ['MHz number of your experimental spectrometer setup'] 
 
 $OPTICAL ROTATION PROPERTY SETTINGS:
 $PART5 SETTINGS:
 optical_rotation: off            # ['on', 'off'] 
 funcOR: pbe                      # ['functional for opt_rot e.g. pbe'] 
 funcOR_SCF: r2scan-3c            # ['functional for SCF in opt_rot e.g. r2scan-3c'] 
 basisOR: def2-SVPD               # ['basis set for opt_rot e.g. def2-SVPD'] 
 frequency_optical_rot: [589.0]   # ['list of freq in nm to evaluate opt rot at e.g. [589, 700]'] 
 $END CENSORC




| This is modification of crest. It is enough to for computation of NMR spectrum.
| Save as cregen.sh filename in your ~/.local/bin/ and rum "chomod +x cregen.sh" to change mode to executive file.

.. code-block:: bash

 #!/bin/bash
 crest isomers.xyz --cregen isomers.xyz --rthr 0.25 --bthr 0.02 --ethr 0.10 --ewin 4.0 > clusters.out
 cp crest_ensemble.xyz clusters.xyz
