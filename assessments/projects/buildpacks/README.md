# Cloud Native Buildpacks Joint Security Assessment

Date completed: Sep 7, 2021

Security reviewers: Andres Vega, Adith Sudhakar, Cole Kennedy, Daniel Papandrea, Daniel Tobin, Magno Logan, Matthew Giasa, Matt Jarvis.

Buildpacks team: Stephen Levine, Sambhav Kothari.

Project Web site: [buildpacks.io](https://buildpacks.io/)

Source code repository: [github.com/buildpacks](https://github.com/buildpacks) 

Core implementation: https://github.com/buildpacks/lifecycle 

Specification: https://github.com/buildpacks/spec 	

Project Web site: [buildpacks.io](https://buildpacks.io/)


## Background

The Cloud Native Buildpacks project provides tooling to transform source code into container images using modular, reusable build functions called _buildpacks_. The project takes advantage of advanced features in the OCI image standard that are underutilized in the Dockerfile model.

The project’s advanced maturity and adoption is showcased by its maintainers adherence to secure software development best practices.

## Maturity and ecosystem adoption

Buildpacks can build container images that can be deployed in Kubernetes and all other container orchestation platforms that are conformant with OCI standards. Notably, Buildpacks can be configured to execute securely on such platforms. The thriving ecosystem surrounding the project evidences ease of extensibility and integration. 

Known vendors that provide buildpacks include Paketo, Heroku, and Google Cloud. Individual communities and vendors can provide buildpacks, which they may publish to the Buildpack Registry.  This is not an exclusive list and it’s likely that there are other vendors that also publish Buildpacks.

Buildpacks is used by numerous other projects and services. This includes Kubernetes Native Container Build Service (kpack), VMware Tanzu Build Service, Weave FireKube, Azure Spring Cloud, Project Riff, Azure Container Registry, Salesforce Evergreen, Google Cloud Run Button, Google kf, Google Skaffold, Spring Boot, Heroku, Gitlab, Dokku, Deft, and Porter. 

## Summary

**Design**: The design of Cloud Native Buildpacks exhibits evidence that the project has been architected from the ground up with special consideration to security aspects. 

Covering many use cases of platform operation and application development, buildpacks tooling manages to abstract unnecesary complexity away from its users while managing to impart a number of security guarantees. Buildpacks ensures that container images generated using its tooling meet a minimum security standard; (1) All processes must use a non-root UID/GID, (2)Build-time and runtime base images are always specified separately, so that build-time dependencies such as compilers are not included in the image, (3) Build-time and runtime environment variables are always specified separately, so that sensitive build-time configuration is not included in the image (4). Container images generated by CNB tooling must contain metadata for auditing. Also, where reproducibility is supported, build packs ensures bit-by-bit reproducibility. 

**Analysis**: The project has done due diligence in security and threat modeling. The security workflow is evidently rigorous. During the assessment process, the project attained a CII Best Practices badge by meeting all the passing criteria. Recently the project team has started signing lifecycle images using [sigstore Cosign](https://github.com/sigstore/cosign) and generating CycloneDX SBoMs for their releases. 

All questions from reviewers were addressed in [self-assessment](self-assessment.md) with non-critical issues or concerns. 

## Recommendations

### Recommendations to the project team

Continue to work towards the next level (silver) Core Infrastructure Best Practices badge.

### Recommendations to the CNCF

Buildpacks possess stronger security guarantees when compared to ecosystem alternatives. Additionally, given buildpacks “in-place upgrade capabilities”, CNB can shorten the time to patch bugs and address security issues across large fleets of images exponentially faster. The assessment team strongly suggests elevating awareness of the project. The assessment team also determines the project is in good position to benefit from a formal third party security audit. 


