# sandbox
Deployment strategy testing repo

## Branches/Environments
### Master 
auto-deploys to Production Server
Connected to Production Database 

### Staging 
auto deploys to stage.pstrax.com?
Is a mirror of the production server with the addition of new features scheduled for the next release that have already been thoroughly tested
Connected to Production Database to test features against production data (Testing Load times for San Diego and whatnot)

### Test
auto deploys to ?
Is a mirror of staging with the addition of stories that have been delivered and are awaiting testing by The Requester (Nathan)
Connected to Staging Database to allow for test data

### Development
auto deploys to ?
Is a mirror of Test of with the addition of any stories that we're currently testing ourselves.
Connected to Staging Database to allow for test data


## Deployment Strategy
Branches (features, enchancements, bug fixes, ) are branched from 'test' 
(Checkout the 'test' branch then run "git checkout -b 'feature/featurename'")
Merge branch into Development and self-test the bug fix or feature
Merge branch into Test once it is completed and ready for testing. Deliver appropriate stories in Pivotal Tracker to notify the Requester to start testing.
Once the Requester approves the story/bugfix create a PR to merage the branch into staging. If needed test the feature on staging against production data. Update release note for next scheduled release. 

When the release is ready we create a PR to merge Staging into Master (Production). Staging branch should be frozen for a few days to ensure no bugs have made it ito production. If a bug is found in production we create a hot fix. If that bug is critical we rollback to the previous release while the bug is being resolved. If the bug is minor just work on the hot fix.  

### Hot Fixes
Hot fixes should be branched off from the staging branch, fixed locally and then pushed back into staging to review as staging is the closest mirror of production. Once the issue is resolved in staging we would create another PR to merge staging into master.   
