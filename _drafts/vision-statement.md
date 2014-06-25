# What is Hydramata?

Hydramata is a framework for developing institutional repositories. The reference implementation of this framework will provide a minimally functional institutional repository system by supporting the upload, preservation, and discovery of an institution’s faculty and student scholarly output of enduring value.

The architecture of Hydramata acknowledges that each institution’s implementation is part of a larger ecosystem not merely a standalone application. As such it specifies interfaces from the core system to discrete functional units (components) and provides a reference implementation for each component. Each component can be extended or exchanged according to the needs of an individual institution. Component customization can be shared among like-minded institutions because the interface between the components and the core will remain consistent.

The Hydramata development process is designed to meet the needs of participating institutions while maintaining a commitment to extensible design and community openness. The project is made up of partner institutions who commit development resources to project and participate in feature planning. Current partners include The University of Notre Dame, The University of Virginia, The University of Cincinnati, Indiana University, and Northwestern University.

The combination of the framework and the reference implementation of each module represents the “base IR”.

## What are the functional requirements for a “base” IR?

The initial development of Hydramata will deliver a Minimal Viable Product (MVP). It is not an exhaustive list of requirements but rather the kinds of things we need the system to do and in what way (configurable?) in preparation for re-architecture planning. The below number represents epics or a number of epics per heading.

### 1. Users can log in using credentials provided by the implementing institution

- Primary users include: Faculty, delegates, students, and library  support staff
- The Hydramata authentication system should be able to integrate with common systems like: LDAP, CAS, or Shibboleth.
- Hydramata should allow the authentication of collaborators external to the implementing institution either through federation, e.g. Shibboleth, or by supporting distributed authorization providers e.g. ORCID.

### 2. The accuracy, persistence, security, and recoverability of what users upload will be maintained throughout the system.

Users and content administrators should be confident that:

- The Hydramata application will not change metadata or digital objects inadvertently or unintentionally.
- Hydramata can accommodate an institution’s security precautions to prevent malicious tampering of content e.g. using an anti-virus scanner to prevent the upload of malware.
- Hydramata relies on the preservation methods and actions that Fedora provides including checksums of datastreams.
- Access rights, auditability, and compliance will be maintained transparently.

### 3. I want users to upload _stuff_- either via UI or via a batch process

- Faculty, students are the primary content providers/authors
- Library archival collections are not the target audience for a self-deposit system
- Typical work types would include things like, for which we will have reference implementations of (that can be customized):
	- Image
	- Document
	- ETD
	- Dataset/Database
	- Article
	- Video/Audio
	- Software
- Some works may reference external content instead of or in addition to containing files.
- It should be easy for an implementer to be able to add work types.
- upload a variety of files
	- wide variety of files should be supported for works mentioned above to be downloaded by end user
	- no specialized viewers are included; for example you can download files, Hydramata itself will not include the ability to stream media but does not prevent its implementation.
	- upload from desktop, cloud services
	- upload large files wouldn’t happen via browser but could be accommodated by a sys admin (well over 1 GB)
	- can be possible to upload more than one file to the same work at once
- upload a batch of files where an authorized user (such as a sys admin, repo manager) submits a package to create many works at once outside of the UI.

### 4. I need varied terms of use and license agreements for the stuff I’m uploading

- Standard set of options for choosing a license to apply to a work and the files within the work. That license chosen is persisted in the repository for auditing purposes.
- I want clear understanding of the terms of use for the repository.

### 5. I want them to describe stuff

- There is a default set of fields available for several work types that are included in the reference implementation. Any edits to this work type are done by institution.
- For the reference implementation work types, RDF is optimized to include controlled vocabularies and to support vocabularies expressed as Linked Open Data
- The type of work dictates the available metadata fields
- Any additional work types are able to be added without “too much pain”

### 6. I want to organize stuff, for example

- create groupings of works in the repository (includes their own stuff and users stuff, assuming they can discover it)
- relate works to works

### 7. I want them to be able to share stuff (or restrict from) with the right people such as

- the world
- to a specific person
- to a group
	- that I created
	- that exist in the institution (Hydramata should have the ability to connect to systems so hydramata users can restrict access to specific groups that exist in external system. The two systems we will definitely need to connect to are LDAP and SHIBBOLETH)
- my institution
- an external collaborator
- for a limited amount of time
	- embargo (can’t see until)
	- lease (see until a certain date)
	- one time use URL

### 8. I want them to be able to discover stuff - if they should

- searching and browsing all content in the repository one should discover
- the ability to set different access levels for metadata vs content/files.

### 9. I want them to be able to view stuff

- can view works and download files only if they have the right to
- no specialized viewers should be included in base, you can download files, but we won’t stream media for example

### 10. Users can collaborate on stuff at the item level

- for example, grant edit privileges to other individuals and groups

### 11. I want them to know metrics about their deposits

- users can see basic metrics for content downloads

### 12. I want a variety of roles for people to interact with the IR

- For example, a Repository Manager role should be discover and edit all content in any status. ETD administrator is another example where ETDs would be the only content they could administer
- a few common roles would be included in base.
- there is a way to add people to that role dynamically.
- modifying the role capabilities would need to be possible but does not assume an interactive UI to do.
- other roles needed are up to the institution to create.
- there is no interactive UI to easily create roles
- Hydramata enforces roles and permissions so that only authorized users can change what has been uploaded.

### 13. Contributors names should be able to link to standard identifiers e.g. ORCID

- standard identifiers (ORCID) can be used to clearly identify authors, creators and contributors
- can be used to link to external sources of user information
- local institutions would be responsible for integrating the [ORCID gem](https://github.com/projecthydra-labs/orcid) if they are interested in minting ORCIDs from within the app

### 14. I want Hydramata to be able to integrate an external DOI so I can assign an DOI to works.

- local institutions would be responsible for integrating with external DOI systems if they want to mint DOI’s from within the app similar to [Hydra Remote Identifier](https://github.com/projecthydra-labs/hydra-remote_identifier)
