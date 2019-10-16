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
Lab Tools and Lab Applications are also dependent on the latest releases and not generally
backwards compatible.  The released bundle associates the versions that have been tested together.

There are no requirements changes, major behavioral changes, or major API changes in this release.

#### Summary of FSW changes ####
- Refactor OSAL to reduce code duplication
- Deconflicted performance IDs in lab applications
- Fixed various typos in variables, comments, prints
- Removed CVS flags
- Replaced deprecated references
- Resolved various build and static analysis warnings
- Improved 64 bit support in tools (now default configuration)
- Updated to VxWorks 6.9 support
- Updated to RTEMS 4.11 support
- Startup now fails if OS API initialization fails
- Update PSP timebase support
- Removed CFE_PSP_SUBMINOR_VERSION define
- Minor bug fixes
  - PSP
    - Resolved race condition in PSP timer callbacks
    - Fixed MCP750 FPU exception behavior
    - String manipulation fixes
    - Removed OS_printf calls prior to OS_API_Init

#### Document and Other Non-FSW Updates ####
- Removed non-ascii characters in text files
- Improvements to version control ignore lists
- Scripts set as executable
- Removed unused files/directories
- Removed classic build support in favor of cmake (and updated support where needed)
- Updated directory names
- Added unit test stub functions where needed

#### Marked for Deprecation (will be removed in future release) ####
Define OSAL_OMIT_DEPRECATED and CFE_OMIT_DEPRECATED_6_6 to check for compliance.
In general, replacements are detailed in associated API headers or are no longer needed by underlying software.

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
  - Note cES1702.2 and cES1703.3 were tested when PSP issue #77 was resolved with custom setup (not part of
  build verification)
- Time client configuration requirements that are not supported by the test hardware:
  - cTIME2012.1; cTIME2013; cTIME2014; cTIME2701; cTIME2702; cTIME2703

#### Other Targets ####
This code was also built for and executed on the following targets:
-	Ubuntu 18.04 x86 64 bit
-	Docker Alpine Linux x86 64 bit ( using OSAL_DEBUG_PERMISSIVE_MODE )
-	Raspberry Pi armv6 32 bit ( equivalent of Debian 9)
-	Raspberry Pi Docker armv6 32 bit Alpine Linux ( using OSAL_DEBUG_PERMISSIVE_MODE )

### 1.2 NEW/CHANGED FSW IN THIS VERSION ###

#### 1.2.3 PSP Closed to Version 1.4.0: https://github.com/nasa/psp/issues?q=milestone%3A1.4.0 ####
- 1.4.0 Updates done internally on Babelfish (no GitHub pull references)
  - Merge and Commit are Babelfish references, Issues are GitHub references (transfered from Babelfish)

Merge | Commit | Issue | Summary | Contributor
-- | -- | -- | -- | --
5df03c6 | 67f3d1f | [#109](https://github.com/nasa/psp/issues/109) | Use C99 bool/true/false | jphickey
5df03c6 | 9f873e0 | [#105](https://github.com/nasa/psp/issues/105) | Scrub cfe_platform_cfg.h References | jphickey
5df03c6 | 8ebf0aa | [#104](https://github.com/nasa/psp/issues/104) | Remove CFE_PSP_SUBMINOR_VERSION Define | skliper
b54acc6 | 5ac3a2a | [#106](https://github.com/nasa/psp/issues/106) | Remove ENHANCED_BUILD Switch | jphickey
bf35c18 | 94f4474 | [#101](https://github.com/nasa/psp/issues/101) | Remove CVS Flags | skliper
183a8f3 | 8a38cd6 | [#28](https://github.com/nasa/psp/issues/28) | PSP Panic if OS_API_Init Fails | jphickey
183a8f3 | cd39b8c | [#99](https://github.com/nasa/psp/issues/99) | Remove OS_printf Calls Prior to OS_API_Init | jphickey
22276f8 | cdee882 | [#84](https://github.com/nasa/psp/issues/84) | Replace Deprecated References | jphickey
22276f8 | 59f6d56 | [#27](https://github.com/nasa/psp/issues/27) | Integrate Timebase | jphickey
22276f8 | 6c46c00 | [#85](https://github.com/nasa/psp/issues/85) | Update for RTEMS 4.11 | jphickey
d922b34 | 13df2ae | [#90](https://github.com/nasa/psp/issues/90) | Fix String Manipulation | jphickey
7b806e1 | 5950142 | [#77](https://github.com/nasa/psp/issues/77) | Fix MCP750 FPU Exception Behavior | sseeger
ba64c8e | 43b74ee | [#82](https://github.com/nasa/psp/issues/82) | Resolve Build Warnings | jphickey
22276f8 | 52bdad0 | [#68](https://github.com/nasa/psp/issues/68) | Pass ModuleID to PSP Module Init Function | jphickey

#### 1.2.4 cFS-GroundSystem Closed to Version 2.1.0: https://github.com/nasa/cFS-GroundSystem/issues?q=milestone%3A2.1.0 ####
- 2.1.0 Integration Candidate: https://github.com/nasa/cFS-GroundSystem/pull/26

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#25](https://github.com/nasa/cFS-GroundSystem/pull/25) | [#24](https://github.com/nasa/cFS-GroundSystem/issues/24) | Use SendUdp Header File | avan989
[#23](https://github.com/nasa/cFS-GroundSystem/pull/23) | [#4](https://github.com/nasa/cFS-GroundSystem/issues/4) | Removed Unused Variable | avan989
[#22](https://github.com/nasa/cFS-GroundSystem/pull/22) | [#12](https://github.com/nasa/cFS-GroundSystem/issues/12) | Resolve Build Warnings | avan989
[#19](https://github.com/nasa/cFS-GroundSystem/pull/19) | [#5](https://github.com/nasa/cFS-GroundSystem/issues/5) | Replace gethostbyname Use | avan989

#### 1.2.5 elf2cfetbl Closed to Version 3.1.0: https://github.com/nasa/elf2cfetbl/issues?q=milestone%3A3.1.0 ####
- 3.1.0 Integration Candidate: https://github.com/nasa/elf2cfetbl/pull/13

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#11](https://github.com/nasa/elf2cfetbl/pull/11) | [#8](https://github.com/nasa/elf2cfetbl/issues/8) | Replace Deprecated References | skliper

- Imported Change From Babelfish

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#10](https://github.com/nasa/elf2cfetbl/pull/10) | [#7](https://github.com/nasa/elf2cfetbl/issues/7) | 64 Bit and Updated Machine Support | the-other-james

#### 1.2.6 tblCRCTool Closed to Version 1.1.0: https://github.com/nasa/tblCRCTool/issues?q=milestone%3A1.1.0 ####
- 1.1.0 Integration Candidate: https://github.com/nasa/tblCRCTool/pull/12
  - Note the updates were refactored in the integration candidate, so the original pull requests aren't referenced.

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#12](https://github.com/nasa/tblCRCTool/pull/12) | [#10](https://github.com/nasa/tblCRCTool/issues/10) | Cmake Build Compatibility | avan989
[#12](https://github.com/nasa/tblCRCTool/pull/12) | [#2](https://github.com/nasa/tblCRCTool/issues/2) | Resolve Build Warnings | avan989
[#12](https://github.com/nasa/tblCRCTool/pull/12) | [#1](https://github.com/nasa/tblCRCTool/issues/1) | Close File Descriptor | avan989

#### 1.2.7 ci_lab Closed to Version 2.3.0: https://github.com/nasa/ci_lab/issues?q=milestone%3A2.3.0 ####
- 2.3.0 Integration Candidate: https://github.com/nasa/ci_lab/pull/12

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#11](https://github.com/nasa/ci_lab/pull/11) | [#3](https://github.com/nasa/ci_lab/issues/3) | Deconflict Performance IDs | avan989
[#9](https://github.com/nasa/ci_lab/pull/9) | [#4](https://github.com/nasa/ci_lab/issues/4) | Remove CVS Flags | avan989
[#8](https://github.com/nasa/ci_lab/pull/8) | [#7](https://github.com/nasa/ci_lab/issues/7) | Replace Deprecated References | skliper

#### 1.2.8 sample_app Closed to Version 1.1.0: https://github.com/nasa/sample_app/issues?q=milestone%3A1.1.0 ####
- 1.1.0 Integration Candidate: https://github.com/nasa/sample_app/pull/11

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#9](https://github.com/nasa/sample_app/pull/9) | [#3](https://github.com/nasa/sample_app/issues/3) | Remove CVS Flags | avan989
[#7](https://github.com/nasa/sample_app/pull/7) | [#6](https://github.com/nasa/sample_app/issues/6) | Replace Deprecated References | skliper

#### 1.2.9 sample_lib Closed to Version 1.1.0: https://github.com/nasa/sample_lib/issues?q=milestone%3A1.1.0 ####
- 1.1.0 Integration Candidate: https://github.com/nasa/sample_lib/pull/6

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#4](https://github.com/nasa/sample_lib/pull/4) | [#1](https://github.com/nasa/sample_lib/issues/1) | Remove CVS Flags | avan989

#### 1.2.10 sch_lab Closed to Version 2.3.0: https://github.com/nasa/sch_lab/issues?q=milestone%3A2.3.0 ####
- 2.3.0 Integration Candidate: https://github.com/nasa/sch_lab/pull/13

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#10](https://github.com/nasa/sch_lab/pull/10) | [#1](https://github.com/nasa/sch_lab/issues/1) | Deconflict Performance IDs | avan989
[#8](https://github.com/nasa/sch_lab/pull/8) | [#3](https://github.com/nasa/sch_lab/issues/3) | Remove CVS Flags | avan989
[#7](https://github.com/nasa/sch_lab/pull/7) | [#6](https://github.com/nasa/sch_lab/issues/6) | Replace Deprecated References | skliper

#### 1.2.11 to_lab Closed to Version 2.3.0: https://github.com/nasa/to_lab/issues?q=milestone%3A2.3.0 ####
- 2.3.0 Integration Candidate: https://github.com/nasa/to_lab/pull/13

Pull | Issue | Summary | Contributor
-- | -- | -- | --
[#12](https://github.com/nasa/to_lab/pull/12) | [#1](https://github.com/nasa/to_lab/issues/1) | Deconflict Performance IDs | avan989
[#11](https://github.com/nasa/to_lab/pull/11) | [#3](https://github.com/nasa/to_lab/issues/3) | TO_Subscription_t Typo | avan989
[#9](https://github.com/nasa/to_lab/pull/9) | [#4](https://github.com/nasa/to_lab/issues/4) | Remove CVS Flags | avan989
[#8](https://github.com/nasa/to_lab/pull/8) | [#7](https://github.com/nasa/to_lab/issues/7) | Replace Deprecated References | skliper

### TBD ###
