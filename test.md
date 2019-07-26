# List example

<!-- MDLISTTAB_START -->
# Android Data Protection Solutions

 * Project: Solution1 [^ref1]
   * Android (kernel) versions: 2.1
   * Granularity: File
   * Req. App. Changes: Limited to SMS, MMS, Email
   * Req. Sys. Changes: YES
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

 * Project: Solution2 [^ref2]
   * Android (kernel) versions: 2.2.1 (2.6.32)
   * Granularity: Two groups of Apps
   * Approach: Android middleware isolation + Tomoyo
   * Req. App. Changes: NO
   * Req. Sys. Changes: YES
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

 * Project: Solution3 [^ref3]
   * Android (kernel) versions: 2.1
   * Granularity: App
   * Approach: Application level policy to control other app access
   * Req. App. Changes: YES (adds a policy)
   * Req. Sys. Changes: YES (Partially)
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

 * Project: Solution4 [^ref4]
   * Android (kernel) versions: 4.0.4
   * Granularity: Groups of Apps + system service data
   * Approach: Policy based Android middleware + kernel hardening
   * Req. App. Changes: NO
   * Req. Sys. Changes: YES
   * Trusts App: NO
   * Trusts System: YES
   * Trusts Hardware: YES

<!-- MDLISTTAB_END -->
