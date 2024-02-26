# Shiny Apps

These are apps developed by [Brian Yandell](https://github.com/byandell).
Note that repos in the github organization may be behind those in Yandell's repo.

## App Updates

App code in repo [foundr](https://github.com/byandell/foundr) is now at version 1.3.

A few changes:

- Options have been moved closer to their use to make it more intuitive/readable.
- Response on some panels (Traits, Times) now has option “normed” (see below).
- Signal option has been removed as it was too confusing.
- Order traits by option has “p_” removed from p.value choices; default is now “strain”.

A few known bugs:

- Solved panel switching that wiped out dataset choice.
- Not sure SDs are correctly scaled for volcano plots of Stats and Contrasts.
- Default ordering is now by `strain` but may change later to be `strain:diet` for the Diet apps;
this has to do with removing the `signal` choice.

## Data Updates
- Data has not been updated yet. I will update harmonized data when I have time, probably next week. This includes the plasma metabolite data provided by Qiushi and hand-curated by Mark, which is not in the Diet app yet.
- Plan is to redo all harmonized data so that “raw” data (provided by you all in researchdrive) will be the app “value” response, and “normed” will be normal scores of “value” (preserving mean and SD). This only affects the Traits and Times panels. For now, “value” and “normed” will appear similar.
- Victor is working on data protocols. But for now on trait inclusion:
  + My protocol for trait inclusion has been to include traits that have all main effects and interactions present. That is, a trait needs to have 2 levels for each main effect (strain, diet, sex) and for each interaction.
  + I realize that some of you have other data inclusion approaches, but those have not been clearly stated in written instructions (not just email or hallway conversation) that can be readily codified.

## Shiny Apps

- <https://connect.doit.wisc.edu/FounderCalciumStudy/>
- <https://connect.doit.wisc.edu/FounderDietStudy/> (requires key)
- <https://connect.doit.wisc.edu/FounderLiverDietStudy/> (requires key)

## Repos for Shiny Apps

- [foundr](https://github.com/byandell/foundr): package for Founder Shiny Apps
- [FounderDietStudy](https://github.com/byandell/FounderDietStudy): code specific to Founder Diet Study
  + [FounderCalciumStudy](https://github.com/byandell/FounderCalciumStudy): code specific to Founder Calcium Study
  + [modulr](https://github.com/byandell/modulr): package to process WGCNA modules
  + [DO_Diet](https://github.com/byandell/DO_Diet): DO QTL2 Study code
