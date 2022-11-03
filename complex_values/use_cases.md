# Complex values use cases

## Humboldt Extension (draft addition to Darwin Core)

Submitted by Wesley Hochachka, eBird, 2022-11-02

Observations of organisms are essentially always imperfect in the sense that not all individuals that are present within the surveyed region are detected during an observation/collection process.  One of the major components of analyses of biodiversity-observation data is to account for this imperfect detection.  Variation in the probability of detection can be thought of as being a function of observation/collection "effort", with greater effort leading to a greater proportion of individual organisms actually being detected (i.e. increased detection rate).  Different observation/collection processes will have different measures of effort, and often multiple and independent measures of effort will exist.  An example of this is with data collected by the citizen science project eBird (https://ebird.org/home), for which experience has led us to identify 4 separate facets to observation effort that are important for describing variation in detection rate: duration of observation periods, distance travelled during the observation period, area searched within the observation period, and the number of observers within the group that was making observations.  Only one of these 4 facets of effort is described within by Darwin Core by dedicated terms: duration of the observation is covered by the two Darwin Core terms eventDuration and eventDurationUnits.  The other three do not have dedicated fields that describe variation in these aspects of effort (although kludges could be used to force this information into various fields in the existing Darwin Core and the current proposal for the Humboldt Extension to Darwin Core).  While eBird has these four facets of effort, other forms of data collection will have different measures of effort that also will not have dedicated terms.  Rather than trying to create terms for all possible measures of effort, I suspect that the more logical and generalizable way of incorporating information on these three aspects of effort will be to fit them into the pair of terms within the Humboldt Extension: samplingEffortValue and samplingEffortUnit.  Effectively, allowing placement of multiple types of effort information within these two Humbolt Extension terms is the equivalent of creating a sub-table within a database that is dedicated to store the information on observation/collection effort.  I believe that it makes sense to store all potential information about effort as a unit because these effort data all would need to be accessed and used in the same way by anyone fitting models to the data.  To my mind, the major question remaining is whether there is a standardized form in which we can suggest that these multiple data types should be stored as a unit within a single term/database field?

## Author information

Steve Baskauf

## Multiple life stages in museum sample

https://github.com/tdwg/dwc-qa/issues/192

## Latimer Core

Ben Norton

----
Revised 2022-11-03
