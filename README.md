# PAPI ROCm component
```
PAPI ROCm component is a PAPI backend providing access to
AMD GPUs mative perf-counters and metrics.
The component is an adapter for ROCm profiling library API
(RPL, 'ROC-profiler'):
https://github.com/ROCmSoftwarePlatform/rocprofiler

It is going to be a part of Performance API (PAPI),
University of Tennessee, http://icl.utk.edu/papi/
```
The component source tree:
 - README.md - this readme file
 - rocm - PAPI ROCM component
   - README - the component README file
   - Rules.rocm - the component building rules
   - linux-rocm.c - the component C sources

## To install
```
 - Need ROCm installed

 https://github.com/RadeonOpenCompute/ROCm

 - Clone papi repository:

 git clone https://bitbucket.org/icl/papi.git

 - Copy 'rocm' directory to '<your path>/papi/src/components'.
```

## To build
```
  cd <your path>/papi/src
  ./configure --with-components="rocm" 
  make

 - Check PAPI documentation and './configure --help' for other build and
   configure flags like '--with-debug', '--prefix=<prefix path', etc..
 - You can set compiler using CC and CXX env variables.
  For example:

  export CXX=/usr/bin/clang++
  export CC=/usr/bin/clang

 - You can set path to ROCm root by ROCM_DIR and ROCn profiling library,
  ROC-profiler by RPL_DIR.
  By default ROCM_DIR='/opt/rocm' and RPL_DIR='/opt/rocm/rocprofiler':

  export ROCM_DIR=<your path>/rocm
  export RPL_DIR=<your path>/rocprofiler
```

## To test
```
# path to metrics XML file
export ROCP_METRICS=/opt/rocm/rocprofiler/lib/metrics.xml
# path to rocprofiler library
export LD_LIBRARY_PATH=/opt/rocm/rocprofiler/lib:${LD_LIBRARY_PATH}
# simple tests provided by PAPI utils
./utils/papi_component_avail
./utils/papi_native_avail
./utils/papi_command_line rocm:::device:0:GRBM_COUNT rocm:::device:0:GRBM_GUI_ACTIVE
```

## Provided metrics
```
===============================================================================
 Native Events in Component: rocm
===============================================================================
| rocm:::device:0:GRBM_COUNT                                                   |
|            Tie High - Count Number of Clocks                                 |
--------------------------------------------------------------------------------
| rocm:::device:0:GRBM_GUI_ACTIVE                                              |
|            The GUI is Active                                                 |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_WAVES                                                     |
|            Count number of waves sent to SQs. (per-simd, emulated, global)   |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_VALU                                                |
|            Number of VALU instructions issued. (per-simd, emulated)          |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_VMEM_WR                                             |
|            Number of VMEM write instructions issued (including FLAT). (per-si|
|            md, emulated)                                                     |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_VMEM_RD                                             |
|            Number of VMEM read instructions issued (including FLAT). (per-sim|
|            d, emulated)                                                      |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_SALU                                                |
|            Number of SALU instructions issued. (per-simd, emulated)          |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_SMEM                                                |
|            Number of SMEM instructions issued. (per-simd, emulated)          |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_FLAT                                                |
|            Number of FLAT instructions issued. (per-simd, emulated)          |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_FLAT_LDS_ONLY                                       |
|            Number of FLAT instructions issued that read/wrote only from/to LD|
|            S (only works if EARLY_TA_DONE is enabled). (per-simd, emulated)  |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_LDS                                                 |
|            Number of LDS instructions issued (including FLAT). (per-simd, emu|
|            lated)                                                            |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INSTS_GDS                                                 |
|            Number of GDS instructions issued. (per-simd, emulated)           |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_WAIT_INST_LDS                                             |
|            Number of wave-cycles spent waiting for LDS instruction issue. In |
|            units of 4 cycles. (per-simd, nondeterministic)                   |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_ACTIVE_INST_VALU                                          |
|            Number of cycles the SQ instruction arbiter is working on a VALU i|
|            nstruction. (per-simd, nondeterministic)                          |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_INST_CYCLES_SALU                                          |
|            Number of cycles needed to execute non-memory read scalar operatio|
|            ns. (per-simd, emulated)                                          |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_THREAD_CYCLES_VALU                                        |
|            Number of thread-cycles used to execute VALU operations (similar t|
|            o INST_CYCLES_VALU but multiplied by # of active threads). (per-si|
|            md)                                                               |
--------------------------------------------------------------------------------
| rocm:::device:0:SQ_LDS_BANK_CONFLICT                                         |
|            Number of cycles LDS is stalled by bank conflicts. (emulated)     |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_TA_BUSY                                                   |
|            TA block is busy. Perf_Windowing not supported for this counter.  |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_FLAT_READ_WAVEFRONTS                                      |
|            Number of flat opcode reads processed by the TA.                  |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_FLAT_WRITE_WAVEFRONTS                                     |
|            Number of flat opcode writes processed by the TA.                 |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_HIT                                                      |
|            Number of cache hits.                                             |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MISS                                                     |
|            Number of cache misses. UC reads count as misses.                 |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MC_RDREQ                                                 |
|            Number of 32-byte reads. The hardware actually does 64-byte reads |
|            but the number is adjusted to provide uniformity.                 |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MC_WRREQ                                                 |
|            Number of 32-byte transactions going over the TC_MC_wrreq interfac|
|            e. Atomics may travel over the same interface and are generally cl|
|            assified as write requests.                                       |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MC_WRREQ_STALL                                           |
|            Number of cycles a write request was stalled.                     |
--------------------------------------------------------------------------------
| rocm:::device:0:TCP_TA_DATA_STALL_CYCLES                                     |
|            TCP stalls TA data interface. Now Windowed.                       |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_BUSY_avr                                                  |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_BUSY_max                                                  |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_BUSY_min                                                  |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_FLAT_READ_WAVEFRONTS_sum                                  |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TA_FLAT_WRITE_WAVEFRONTS_sum                                 |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_HIT_sum                                                  |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MISS_sum                                                 |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MC_RDREQ_sum                                             |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_MC_WRREQ_sum                                             |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:TCC_WRREQ_STALL_max                                          |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:FETCH_SIZE                                                   |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:WRITE_SIZE                                                   |
|                                                                              |
--------------------------------------------------------------------------------
| rocm:::device:0:GPUBusy                                                      |
|            The percentage of time GPU was busy.                              |
--------------------------------------------------------------------------------
| rocm:::device:0:Wavefronts                                                   |
|            Total wavefronts.                                                 |
--------------------------------------------------------------------------------
| rocm:::device:0:VALUInsts                                                    |
|            The average number of vector ALU instructions executed per work-it|
|            em (affected by flow control).                                    |
--------------------------------------------------------------------------------
| rocm:::device:0:SALUInsts                                                    |
|            The average number of scalar ALU instructions executed per work-it|
|            em (affected by flow control).                                    |
--------------------------------------------------------------------------------
| rocm:::device:0:VFetchInsts                                                  |
|            The average number of vector fetch instructions from the video mem|
|            ory executed per work-item (affected by flow control). Excludes FL|
|            AT instructions that fetch from video memory.                     |
--------------------------------------------------------------------------------
| rocm:::device:0:SFetchInsts                                                  |
|            The average number of scalar fetch instructions from the video mem|
|            ory executed per work-item (affected by flow control).            |
--------------------------------------------------------------------------------
| rocm:::device:0:VWriteInsts                                                  |
|            The average number of vector write instructions to the video memor|
|            y executed per work-item (affected by flow control). Excludes FLAT|
|             instructions that write to video memory.                         |
--------------------------------------------------------------------------------
| rocm:::device:0:FlatVMemInsts                                                |
|            The average number of FLAT instructions that read from or write to|
|             the video memory executed per work item (affected by flow control|
|            ). Includes FLAT instructions that read from or write to scratch. |
--------------------------------------------------------------------------------
| rocm:::device:0:LDSInsts                                                     |
|            The average number of LDS read or LDS write instructions executed |
|            per work item (affected by flow control).  Excludes FLAT instructi|
|            ons that read from or write to LDS.                               |
--------------------------------------------------------------------------------
| rocm:::device:0:FlatLDSInsts                                                 |
|            The average number of FLAT instructions that read or write to LDS |
|            executed per work item (affected by flow control).                |
--------------------------------------------------------------------------------
| rocm:::device:0:GDSInsts                                                     |
|            The average number of GDS read or GDS write instructions executed |
|            per work item (affected by flow control).                         |
--------------------------------------------------------------------------------
| rocm:::device:0:VALUUtilization                                              |
|            The percentage of active vector ALU threads in a wave. A lower num|
|            ber can mean either more thread divergence in a wave or that the w|
|            ork-group size is not a multiple of 64. Value range: 0% (bad), 100|
|            % (ideal - no thread divergence).                                 |
--------------------------------------------------------------------------------
| rocm:::device:0:VALUBusy                                                     |
|            The percentage of GPUTime vector ALU instructions are processed. V|
|            alue range: 0% (bad) to 100% (optimal).                           |
--------------------------------------------------------------------------------
| rocm:::device:0:SALUBusy                                                     |
|            The percentage of GPUTime scalar ALU instructions are processed. V|
|            alue range: 0% (bad) to 100% (optimal).                           |
--------------------------------------------------------------------------------
| rocm:::device:0:FetchSize                                                    |
|            The total kilobytes fetched from the video memory. This is measure|
|            d with all extra fetches and any cache or memory effects taken int|
|            o account.                                                        |
--------------------------------------------------------------------------------
| rocm:::device:0:WriteSize                                                    |
|            The total kilobytes written to the video memory. This is measured |
|            with all extra fetches and any cache or memory effects taken into |
|            account.                                                          |
--------------------------------------------------------------------------------
| rocm:::device:0:L2CacheHit                                                   |
|            The percentage of fetch, write, atomic, and other instructions tha|
|            t hit the data in L2 cache. Value range: 0% (no hit) to 100% (opti|
|            mal).                                                             |
--------------------------------------------------------------------------------
| rocm:::device:0:MemUnitBusy                                                  |
|            The percentage of GPUTime the memory unit is active. The result in|
|            cludes the stall time (MemUnitStalled). This is measured with all |
|            extra fetches and writes and any cache or memory effects taken int|
|            o account. Value range: 0% to 100% (fetch-bound).                 |
--------------------------------------------------------------------------------
| rocm:::device:0:MemUnitStalled                                               |
|            The percentage of GPUTime the memory unit is stalled. Try reducing|
|             the number or size of fetches and writes if possible. Value range|
|            : 0% (optimal) to 100% (bad).                                     |
--------------------------------------------------------------------------------
| rocm:::device:0:WriteUnitStalled                                             |
|            The percentage of GPUTime the Write unit is stalled. Value range: |
|            0% to 100% (bad).                                                 |
--------------------------------------------------------------------------------
| rocm:::device:0:ALUStalledByLDS                                              |
|            The percentage of GPUTime ALU units are stalled by the LDS input q|
|            ueue being full or the output queue being not ready. If there are |
|            LDS bank conflicts, reduce them. Otherwise, try reducing the numbe|
|            r of LDS accesses if possible. Value range: 0% (optimal)          |
--------------------------------------------------------------------------------
| rocm:::device:0:LDSBankConflict                                              |
|            The percentage of GPUTime LDS is stalled by bank conflicts. Value |
|            range: 0% (optimal) to 100% (bad).                                |
--------------------------------------------------------------------------------

Total events reported: 60
```
