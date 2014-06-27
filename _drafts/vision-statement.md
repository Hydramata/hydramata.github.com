# What is Hydramata?

Hydramata is a framework for developing institutional repositories. The reference implementation of this framework will provide a minimally functional institutional repository system by supporting the upload, preservation, and discovery of an institution’s faculty and student scholarly output of enduring value.

The architecture of Hydramata acknowledges that each institution’s implementation is part of a larger ecosystem not merely a standalone application. As such it specifies interfaces from the core system to discrete functional units (components) and provides a reference implementation for each component. Each component can be extended or exchanged according to the needs of an individual institution. Component customization can be shared among like-minded institutions because the interface between the components and the core will remain consistent.

The Hydramata development process is designed to meet the needs of participating institutions while maintaining a commitment to extensible design and community openness. The project is made up of partner institutions who commit development resources to project and participate in feature planning. Current partners include The University of Notre Dame, The University of Virginia, The University of Cincinnati, Indiana University, and Northwestern University.

The combination of the framework and the reference implementation of each module represents the “base IR”.

## What are the functional requirements for a “base” IR?

The initial goal of Hydramata is to deliver a powerful, flexible  means of storing and retrieving heterogenous data and metadata from a preservation-enabled storage system. On top of this core Hydramata will implement the features necessary to provide a minimal viable product for a self-deposit digital repository. The development of the self-deposit features will not be guided by an exhaustive list of requirements for a digital repository ecosystem. Instead, Hydramata will focus on providing the following features:

### 1. Users can log in using credentials provided by the implementing institution

- Primary users include: Faculty, delegates, students, and library  support staff
- The Hydramata authentication system should be able to integrate with common providers such as: LDAP, CAS, or Shibboleth.
- Hydramata should allow the authentication of collaborators external to the implementing institution either through federation, e.g. Shibboleth, or by supporting distributed authorization providers e.g. ORCID.

### 2. The accuracy, persistence, security, and recoverability of what users upload will be maintained throughout the system.

Users and content administrators should be confident that:

- The Hydramata application will not change metadata or digital objects inadvertently or unintentionally.
- Hydramata can accommodate an institution’s security policies and prevent malicious tampering of content e.g. using an anti-virus scanner to prevent the upload of malware.
- Hydramata relies on the preservation methods and actions that Fedora provides including checksums of datastreams.
- Access rights, auditability, and compliance will be maintained transparently.

### 3. Users can upload content via a web interface or batch process.

- Faculty, students are the primary content providers/authors
- Library archival collections are not the target audience for a self-deposit system
- There will be reference implementations of common work types such as:
	- Image
	- Document
	- ETD
	- Dataset/Database
	- Article
	- Video/Audio
	- Software
- It should be easy for an implementer to be able to add work types.
- Works can reference external content.
- Works can contain one or more files.
	- Files of any type can be uploaded to Hydramata, associated with a work, and be downloaded by an end user.
	- Hydramata will not augment the ability of a web browser to display files; files can downloaded or rendered in the browser when supported. Although Hydramata will not include the ability to stream media or include interactive file viewers it will not prevent their implementation.
	- Files can be uploaded from a User’s computer but will be limited to what can be accommodated by the native browser upload functionality (this has a practical limitation of around .5 Gb)
	- Uploading large files (well over 1 GB) will not be possible could for an end user but could be accommodated by a sys admin.
	- It will be possible to upload more than one file at a time to a work
	- Files in cloud services will be able to be transferred to Hydramata.
- An authorized user (such as a sys admin or repo manager) can batch upload files by submitting a package that will create many works at a time. This will take place outside of the Hydramata web interface.

### 4. There will be appropriate terms of use and license agreements for content added to Hydramata.

- Hydramata will provide a default set of options for licenses that apply to a work and the files within the work. The chosen license will be persisted in the repository for auditing purposes.
- The list of applicable content licenses may differ based on work type.
- The deposit agreement may differ based on administrative context.
- The terms of use for the repository will be stated clearly.

### 5. Content in Hydramata can be described in varying degrees of detail.

- The work type dictates the available form fields for composing or editing metadata.
- There will be reference implementations of several work types. These reference implementations can be customized or extended by an implementer.
- Creating additional work types will be relatively easy.
- If a work is enriched with metadata beyond what fields are defined in the work type (e.g. through a batch process) the extra metadata will not be discarded.

### 6. Content in Hydramata can be organized in a variety of ways.

- Works can be grouped together arbitrarily. Groups of works can contain works from multiple owners.
- Works will be able to be related to each other. This can be a varying levels of specificity e.g. simply ”related“ or using a Group 1 FRBR relationship: exemplarOf, embodymentOf, realizationOf.

### 7. Content in Hydramata can be shared with domains, groups, or individuals for varying lengths of time.

- Domains:
	- The world
	- The implementing institution
- Groups:
	- That are created by an individual
	- That are functional units in an implementing institution. Hydramata will need to integrate with LDAP or Shibboleth in order for users to restrict access to groups that exist in those external systems.
- Individuals:
	- A specific person at an implementing institution
	- An external collaborator with a known ID e.g. ORCID.
- Time bounds:
	- Available immediately
	- Embargo: available until a specified date
	- Lease: available until a specified date
	- Single use URL: available only once at a specific URL

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

### 14. Hydramata will be able to integrate with external identifier providers so that works can be uniquely identified.

- An implementing institution can integrate with services that provide [DOI](http://www.doi.org/), [HDL](http://www.handle.net/), or other identifier schemes.
- [Hydra Remote Identifier](https://github.com/projecthydra-labs/hydra-remote_identifier) is a reference implementation for integrating with a DOI provider.

### 15. Works, Files, and Collections can belong to Administrative Contexts.