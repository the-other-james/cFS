# Version Description Document #
#### core Flight System Framework ####
#### BUILD: 6.7.0 ####
#### RELEASE DATE: TBD ####
#### RELEASED BY: Goddard Space Flight Center ####

## 1.0 FSW VERSION DESCRIPTION ##
### 1.1 PURPOSE AND SUMMARY ###
This is a release of the core Flight System (cFS) Framework elements as follows:
- **core Flight Executive: [cFE](https://github.com/nasa/cFE)** - Version 6.7.0
- **Operating System Abstraction Layer: [OSAL](https://github.com/nasa/osal)** - Version 5.0.0
  - posix
  - rtems (supports 4.11)
  - vxworks (supports 6.9)
- **Platform Support Package: [PSP](https://github.com/nasa/PSP)** - Version 1.4.0 
  - pc-linux
  - pc-rtems
  - mcp750-vxworks
- Lab Tools
  - **Sample Ground System: [cFS-GroundSystem](https://github.com/nasa/cFS-GroundSystem)** - Version 2.1.0
  - **ELF to cFE Table Converter: [elf2cfetbl](https://github.com/nasa/elf2cfetbl)** - Version 3.1.0
  - **Table Cyclic Redundancy Check Tool: [tblCRCTool](https://github.com/nasa/tblCRCTool)** - Version 1.1.0
- Lab Applications
  - **Command Ingest: [ci_lab](https://github.com/nasa/ci_lab)** - Version 2.3.0
  - **Sample Application: [sample_app](https://github.com/nasa/sample_app)** - Version 1.1.0
  - **Sample Library: [sample_lib](https://github.com/nasa/sample_lib)** - Version 1.1.0
  - **Schedular: [sch_lab](https://github.com/nasa/sch_lab)** - Version 2.3.0
  - **Telemetry Output: [to_lab](https://github.com/nasa/to_lab)** - Version 2.3.0

Backwards or cross compatibility is not supported between the cFE, OSAL, and PSP.
Application verification against this version are documented on the https://github.com/nasa/cFS/.

There are no requirements changes, major behavioral changes, or major API changes in this release.

#### Summary of bug fixes and enhancements ####

- Refactor OSAL to reduce code duplication
- Deprecated classic build in favor of cmake
- Deconflicted performance IDs
- Fixed various typos
- Removed CVS flags
- Replaced deprecated references

#### Document and Other Non-FSW Updates ####
- Removed non-ascii characters in text files
- Improvements to version control ignore lists
- Scripts set as executable

#### Unit Testing ####
Unit - steps, results, coverage TBD

VxWorks OSAL coverage TBD

Functional TBD

#### Build Verification Testing ####
The cFE 6.7.0 build was tested by Walt Moleski in the cFS Lab using the mcp750 target with VxWorks 6.9.
Testing was completed on 10/8/2019.

There were 17 Build Verification tests executed and they all passed. Three (3) alternate image configuration
tests were NOT executed since they required a separate compilation of the cFE using different values for 
several configuration parameters as well as introducing changes to the BSP/PSP code. They were the Alternate 
Image test (cfe_AltImage), Object Creation Failure test (cfe_OSObjFailure), and the user-defined exception 
handler test (cfe_myeh).

There were several requirements that were not tested. They are:
- Device Driver requirements are not implemented.
  - cES1324; cES1325; cES1326; cES1326.1; cES1327, cES1508.3
- PSP/BSP and mission configuration dependent requirements:
  - cES1515.1; cES1702.2; cES1702.3; cES1703.2; cES1703.3
- Time client configuration requirements that are not supported by the test hardware:
  - cTIME2012.1; cTIME2013; cTIME2014; cTIME2701; cTIME2702; cTIME2703

#### Other Targets ####
This code was also built for and executed on the following targets:
-	Ubuntu 18.04 x86 64 bit
-	Docker Alpine Linux x86 64 bit ( need to use the OSAL PERMISSIVE_DEBUG option )
-	Raspberry Pi armv6 32 bit ( equivalent of Debian 9)
-	Raspberry Pi Docker armv6 32 bit Alpine Linux ( again PERMISSIVE OSAL_DEBUG )

### 1.2 NEW/CHANGED FUNCTIONALITY IN THIS VERSION ###

#### [1.2.10 sch_lab](https://github.com/nasa/sch_lab) ####
- Integration candidate: https://github.com/nasa/sch_lab/pull/13

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#10](https://github.com/nasa/sch_lab/pull/10) | [#1](https://github.com/nasa/sch_lab/issues/1) | Deconflict Performance IDs | avan989
[#9](https://github.com/nasa/sch_lab/pull/9) | [#4](https://github.com/nasa/sch_lab/issues/4) | Remove Classic Build | avan989
[#8](https://github.com/nasa/sch_lab/pull/8) | [#3](https://github.com/nasa/sch_lab/issues/3) | Remove CVS Flags | avan989
[#7](https://github.com/nasa/sch_lab/pull/7) | [#6](https://github.com/nasa/sch_lab/issues/6) | Replace Deprecated References | skliper

#### [1.2.11 to_lab](https://github.com/nasa/to_lab) ####
- Integration candidate: https://github.com/nasa/to_lab/pull/13

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#12](https://github.com/nasa/to_lab/pull/12) | [#1](https://github.com/nasa/to_lab/issues/1) | Deconflict Performance IDs | avan989
[#11](https://github.com/nasa/to_lab/pull/11) | [#3](https://github.com/nasa/to_lab/issues/3) | TO_Subscription_t Typo | avan989
[#10](https://github.com/nasa/to_lab/pull/10) | [#5](https://github.com/nasa/to_lab/issues/5) | Remove Classic Build | avan989
[#9](https://github.com/nasa/to_lab/pull/9) | [#4](https://github.com/nasa/to_lab/issues/4) | Remove CVS Flags | avan989
[#8](https://github.com/nasa/to_lab/pull/8) | [#7](https://github.com/nasa/to_lab/issues/7) | Replace Deprecated References | skliper

### TBD ###
