## Upload Files

## V1 1/28/2025

(Frame index is always 1 for non videos )

Asumptions:
Logged in, have deployment ready beforeha d

laser calibration images = (checkerboard or dive slate)

validate jwt token on route changes

backend jwt validation checks with database

laser and lens cal are bunch of matrices

let user validate laser detections

validate fish ORF instead of labeling

ask for dive slate pdf and checkerboard specifications

lens cal will be attached to camera and different flow

done by admin of org? camera associated with org?

POST camera / deployement info?

```mermaid
sequenceDiagram
    actor User

    activate User
    activate Frontend
    
    User ->> Frontend: Selects Deployment
    Frontend ->> Frontend: Validate JWT Token 
    Frontend ->> User: Displays deployment page for user
    User ->> Frontend: Presses upload button
    Frontend ->> User: Prompts user to select folder of laser calibration images 

    User ->> Frontend: Selects Folder

    Frontend ->> Frontend: Filter out all files except ORF

    Frontend ->> Frontend: Validate JWT Token

    activate Backend

    Frontend ->> Backend: Post laser calibration ORFS

    activate Database

    Backend ->> Database: Validate JWT Token

    Database ->> Backend: Returns success on validation

    deactivate Database

    Backend ->> Backend: Process laser calibration images and output laser_cals 

    activate Database

    Backend ->> Database: Store laser cal metadata in database

    Database ->> Backend: Returns id

    deactivate Database

    Backend ->> Frontend: Returns 201 created

    deactivate Backend

    Frontend ->> Frontend: Validate JWT token

    Frontend ->> User: Display images and laser_cals for user to validate

    User ->> Frontend: User confirms calibrations are good

    activate Backend

    Frontend ->> Backend: Post validate: True, laser cal id

    activate Database

    Backend ->> Database: Change laser_cal validate parameter from False to True

    Database ->> Backend: Returns success

    deactivate Database

    Backend ->> Frontend: Post 200 success

    deactivate Backend

    Frontend ->> User: Prompts user to select folder of fish images

    User ->> Frontend: Selects Folder

    Frontend ->> Frontend: Filter out all files except ORF

    Frontend ->> Frontend: Validate JWT Token

    activate Backend

    Frontend ->> Backend: Post Fish ORFs

    activate Database

    Backend ->> Database: Validate JWT Token

    Database ->> Backend: Returns success on validation

    deactivate Database

    Backend ->> Backend: Process Fish ORFs

    activate Database

    Backend ->> Database: Store Fish ORFs and lengths

    Database ->> Backend: Return Fish ORF info in database

    deactivate Database

    Backend ->> Frontend: Return 200 and Fish ORFs information

    Frontend ->> User: Displays Fish ORFs and prompt user to validate

    User ->> Frontend: User validates

    

    
 

    deactivate Frontend
    deactivate User
```
