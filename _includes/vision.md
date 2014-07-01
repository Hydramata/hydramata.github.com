UNRATIFIED DRAFT

# What is Hydramata?

Hydramata is a framework for developing institutional repositories. The reference implementation of this framework will provide a minimally functional institutional repository system by supporting the upload, preservation, and discovery of an institution’s faculty and student scholarly output of enduring value.

The architecture of Hydramata acknowledges that each institution’s implementation is part of a larger ecosystem not merely a standalone application. As such it specifies interfaces from the core system to discrete functional units (components) and provides a reference implementation for each component. Each component can be extended or exchanged according to the needs of an individual institution. Component customization can be shared among like-minded institutions because the interface between the components and the core will remain consistent.

The Hydramata development process is designed to meet the needs of participating institutions while maintaining a commitment to extensible design and community openness. The project is made up of partner institutions who commit development resources to project and participate in feature planning. Current partners include The University of Notre Dame, The University of Virginia, The University of Cincinnati, Indiana University, and Northwestern University.

The combination of the framework and the reference implementation of each module represents the “base IR”.

## What are the functional requirements for a “base” IR?

The initial goal of Hydramata is to deliver a powerful, flexible means of storing and retrieving heterogenous data and metadata from a preservation-enabled storage system. On top of this core Hydramata will implement the minimum features necessary to provide a self-deposit enabled digital repository. The development of the self-deposit features will not be guided by an exhaustive list of requirements for a digital repository ecosystem. Instead, Hydramata will focus on providing the following features:

1.  Users can log in using credentials provided by the implementing institution
	1. Primary users include: Faculty, delegates, students, and library support staff
	1. The Hydramata authentication system should be able to integrate with common providers such as: LDAP, CAS, or Shibboleth.
	1. Hydramata should allow the authentication of collaborators external to the implementing institution either through federation, e.g. Shibboleth, or by supporting distributed authorization providers e.g. ORCID.

2. The accuracy, persistence, security, and recoverability of what users upload will be maintained throughout the system.
	1. The Hydramata application will not change metadata or digital objects inadvertently or unintentionally.
	1. Hydramata can accommodate an institution’s security policies and prevent malicious tampering of content e.g. using an anti-virus scanner to prevent the upload of malware.
	1. Hydramata relies on the preservation methods and actions that Fedora provides including checksums of datastreams.
	1. Access rights, auditability, and compliance will be maintained transparently.

3. Users can upload content via a web interface or batch process.
	1. Faculty and students are the primary content providers/authors
	1. Library archival collections are not the target audience for a self-deposit system
	1. There will be reference implementations of common work types such as:
		1. Article
		1. Audio
		1. Dataset
		1. Document
		1. ETD
		1. Image
		1. Software
		1. Video
	1. It should be easy for an implementer to add work types.
	1. Works can reference external content.
	1. Works can contain one or more files.
		1. Files of any type can be uploaded to Hydramata, associated with a work, and be downloaded by an end user.
		1. Files can be uploaded from a user’s computer but will be limited to what can be accommodated by the native browser upload functionality (this has a practical limitation of around .5 GB)
		1. Uploading large files (well over 1 GB) will not be possible via the web interface. Ingesting large files can be accommodated by a sys admin.
		1. A work can have more than one file uploaded to it at once.
		1. Files in cloud services will be able to be transferred to Hydramata.
	1. An authorized user (such as a sys admin or repository manager) can batch upload files by submitting a package that will create many works at a time. This will take place outside of the Hydramata web interface.

4. There will be appropriate terms of use and license agreements for content added to Hydramata.
	1. Hydramata will provide a default set of options for licenses that apply to a work and the files within the work. The chosen license will be persisted in the repository for auditing purposes.
	1. The list of applicable content licenses may differ based on work type.
	1. The deposit agreement may differ based on administrative context.
	1. The terms of use for the repository will be stated clearly.

5. Content in Hydramata can be described in varying degrees of detail.
	1. The work type dictates the available form fields for composing or editing metadata.
	1. There will be reference implementations of several work types. These reference implementations can be customized or extended by an implementer.
	1. If a work is enriched with metadata beyond what fields are defined in the work type (e.g. through a batch process) the extra metadata will not be discarded.

6. Content in Hydramata can be organized in a variety of ways.
	1. Works can be grouped together arbitrarily. Groups of works can contain works from multiple owners.
	1. Works will be able to be related to each other. This can be a varying levels of specificity e.g. simply “related” or using a Group 1 FRBR relationship: exemplarOf, embodymentOf, realizationOf.

7. Content in Hydramata can be shared with domains, groups, or individuals for varying lengths of time.
	1. Domains:
		1. The world
		1. The implementing institution
	1. Groups:
		1. That are created by an individual
		1. That are functional units in an implementing institution. Hydramata will need to integrate with LDAP and/or Shibboleth in order for users to restrict access to groups that exist in those external systems.
	1. Individuals:
		1. A specific person at an implementing institution
		1. An external collaborator with a known ID e.g. ORCID.
	1. Time bounds:
		1. Available immediately
		1. Embargo: available until a specified date
		1. Lease: available until a specified date
		1. Single use URL: available only once at a specific URL

8. Hydramata will provide a search and discovery interface that enforces access controls.
	1. Content can be excluded from the search result listings based on the privileges of the user conducting the search.
	1. Access controls can be set independently at the Work level and the File level.

9. Hydramata will display content.
	1. Each Work will have a detail page enumerating its contents.
	1. Files can be downloaded directly from Hydramata.
	1. Files will be rendered in the browser when supported.
	1. Hydramata will not augment the ability of a web browser to display files.
	1. Hydramata will not include the ability to stream media or include interactive file viewers but it will not prevent their implementation.
	1. The ability to view a Work or download a File will be determined by their respective access controls.

10. Hydramata will facilitate collaborative editing of works.
	1. A depositor may grant editing privileges to other individuals and groups of their choosing at any time.

11. Hydramata will provide basic usage statistics.
	1. Views and downloads of content will be logged for reporting purposes.
	1. A usage summary will be made available to end users e.g. download count for a file.

12. Hydramata will use roles to determine what a user is able to do.
	1. Users can only discover, view, create, or update the content with which they are authorized. Roles are the primary method of granting authorization to a user.
	1. There are use cases for granting privileges to all the content in Hydramata as well as subsets of the content.
		1. A Repository Manager role should be able discover and edit all content in any status.
		1. An ETD Administrator role would grant the ability to discover and edit all content of the ETD work type.
	1. There will be a reference implementation of a Repository Manager.
	1. Additional roles may be created by implementing institutions.
	1. There will be no interactive UI for creating roles.
	1. Individuals must be able to be given roles dynamically.
	1. There must be a way for an implementing institution to modify the abilities granted to a role but it is not necessary to have an interactive UI to do.

13. Names of people within Hydramata can include an external identifier so that individuals can be uniquely identified.
	1. An implementing institution can employ [ORCID](http://orcid.org/), [ResearcherID](http://www.researcherid.com/), [ISNI](http://www.isni.org/), or other identifier schemes to clearly identify authors, creators and contributors.
	1. [ORCID](http://orcid.org/) will be the reference implementation.
	1. The [ORCID gem](https://github.com/projecthydra-labs/orcid) is a reference implementation for creating and authorizing ORCID iDs for their patrons.

14. Hydramata will be able to integrate with external identifier providers so that works can be uniquely identified.
	1. An implementing institution can employ [DOI](http://www.doi.org/), [HDL](http://www.handle.net/), or other identifier schemes to clearly identify content.
	1. [DOI](http://www.doi.org/) will be the reference implementation.
	1. [Hydra Remote Identifier](https://github.com/projecthydra-labs/hydra-remote_identifier) is a reference implementation for integrating with a DOI provider.

15. Works, Files, and Collections can belong to Administrative Contexts.
	1. An administrative context is a way of organizing works, files, and collections in Hydramata.
	1. Administrative contexts may have a subset or a superset of work types available to the general holdings.
	1. Roles can be created that are specific to an administrative context.
	1. Administrative contexts will be represented as facet values in the discovery interface.
		1. Administrative contexts are expected to map to organizational structures in the implementing institution. As such they may be nested in the facet listing. This nesting does not imply permission inheritance from parent administrative contexts to child ones.
