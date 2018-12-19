:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

Introduction
============

The LSST Science Platform (LSP) is a collection of services that can be instantiated multiple times in multiple locations for multiple purposes and user groups.
Some of these services directly support the LSP and are intended to themselves be re-instantiated in every LSP instance.
Other services provide back-end infrastructure and can be shared across multiple LSP instances where appropriate.

This document describes the current LSP instances, the near future deployments, and the expected deployments in Commissioning and Operations.

Use cases for the LSP instances are described in the Confluence page "`Science Platform Instances - a re-evaluation <http://ls.st/t5e>`_".


Present Deployments
===================

Kubernetes Clusters
-------------------

The LSP is deployed on Kubernetes.
There are currently two Kubernetes clusters available, both at NCSA: a large one called the Kubernetes Commons used for development and a much smaller one used primarily for testing new Kubernetes versions.
In addition, the cloud-based Google Kubernetes Engine (GKE) is sometimes used for deployments of the LSP.

LSP Instances
-------------

.. figure:: /_static/LSP_Instances_Today.png
   :name: lsp-today

   LSP instances as of December 2018.

There are two primary instances of the LSP today, both deployed in the Kubernetes Commons.
One is used for integration and science-level validation testing; this is the former ``lsst-pdac`` (for Prototype Data Access Center) that will be renamed ``lsst-lsp-int`` (for integration).
The second is used for Science Pipelines developer investigation and testing by LSST DM staff as well as a mix of non-DM and non-LSST users via demonstrations, boot camps, and the "Stack Club".
It was previously named ``lsst-lspdev`` (indicating its use for Science Pipelines developers) but will be renamed ``lsst-lsp-stable``.

The ``lsst-lsp-int`` instance has long had a Portal Aspect and API Aspect deployed.
Recently a Notebook Aspect was added.
Underlying these, an instance of the Qserv database provides large-scale catalog query service.
This Qserv instance is somewhere between development and integration.
While substantial developer testing can be done on the Qserv cluster at IN2P3, data availability and scale require certain tests to be run at NCSA.
Image datasets have been provided from ``/datasets`` in the common NCSA GPFS filesystem.
The User File Workspace for the Notebook Aspect of the instance is also provided from ``/jhome`` in GPFS.
Authentication is only provided for the Notebook Aspect via CILogon.

The ``lsst-lsp-stable`` instance has only had a Notebook Aspect deployed, with image datasets and the User File Workspace from GPFS and authentication via CILogon.

At times, "pop-up" deployments of the LSP (just the Notebook Aspect) on GKE have been used to support elastic, short-term usage.
Images are copied to the cloud and the User File Workspace is also provided there, with no direct connection to NCSA resources.


Future Deployments
==================

Near Future
-----------

In the near future, a Kubernetes Production cluster will be brought up.
Deployments in this cluster, as well as adjustments to its configuration, will be limited and performed after a change control process to ensure stability.
The ``lsst-lsp-stable`` LSP instance will move into this cluster.
A Portal Aspect will be brought up in this instance as well to provide Firefly visualization services.
There are no current plans to bring up the API Aspect in this instance, but this will happen at some point, along with a database back-end (that need not be Qserv).

Staging Instance
----------------

Later on, as part of the change control process, it is anticipated that a staging instance will be deployed in the Kubernetes Production cluster as a final test before having changes go live in the ``lsst-lsp-stable`` instance.

Kubernetes Test Instance
------------------------

From time to time, an LSP instance will be deployed in the Kubernetes Test cluster, along with a small (single-node or few-node) Qserv cluster for the purpose of ensuring deployment and operation of the LSP functions correctly in new versions of Kubernetes.

Commissioning
-------------

In Commissioning, an LSP instance will be deployed on the Commissioning Cluster at the Base Facility in La Serena, Chile.
That instance will have its own back-end database (non-Qserv) and User File Workspace.

Operations
----------

In Operations, LSP instances will be deployed in the Chilean and US Data Access Centers.

Authentication and Authorization
--------------------------------

Note that even if instances share an authentication service or mechanism, such as CILogon, they are expected to be configured differently, so that different users will be permitted to use each instance, potentially with different authorizations to use its services.

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
