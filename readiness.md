# Beacon release review

## Pipeline audit
Gap / risk / repaired dependency:
Production reviewer control to configure (not demonstrated locally):
Secret handling and scope:

## Traceability
Why PATCH is appropriate:
Candidate image and annotated Git tag:
Record tag -> code commit in PDF using git rev-parse commands.
Image-tag mutability limitation:

## Incident recovery
Evidence and rollback vs forward decision:
Known-good target:
Proposed kubectl command (not executed):
Recovery checks after action:

## Release note and decision
Change scope:
Local validation proof:
Open risk / owner / mitigation:
Current production decision and blocker:
Terraform vs Kubernetes responsibilities:



Original Failure 1:

In release.yml, the pipeline was never validated as the validation was never run in the production, after adding the line ```needs: production``` we were able to a validate the pipeline and pass the first test

Original Failure 2:

In deployment.json, the image version originally specified the latest version of the beacon-service, however the validation test specifically looks for version 2.3.1, therefore we changed the version from latest to v2.3.1

Original Failure 3:

iN rollback.json, it originally rolled back the target image to v2.3.1, however the image is already running on that version, in other words there is no actual rollback occuring, instead we changed the image version to 2.3.0 so it actually gets rolled back when called.