.. meta::
   :description: UP42 going further: platform core concepts
   :keywords: core concepts, blocks, workflows, tasks, projects  

.. _core-concepts:
              
====================================
 Core concepts: Block, Workflow, Job
====================================

Throughout the documentation, we use three core concepts: **Blocks**,
**Workflows** and **Jobs**. This section gives a comprehensive
explanation of these concepts and the role they play in the platform.
You can also find these and other terms in the :ref:`Glossary <glossary>`.

.. _blocks-definition:

Blocks
======

Blocks are the base units of the platform. There are two categories: **Data** and **Processing** blocks.

.. figure:: _assets/data_and_processing_block.png
    :align: center
    :scale: 35 %     
    :alt: Data and processing block diagram

- **Data blocks** deliver satellite images, vector data or any other type of geospatial data that can be used on UP42. An example of a data block is the ``Sentinel-2 Level-1C Full-Scene`` block or the ``Pléiades Streaming`` block.
- **Processing blocks** transform and/or analyze data, e.g. the ``Raster sharpening`` block or the ``NDVI vegetation index`` block.

.. _workflows-definition:

Workflows
=========

A **workflow** is a `Directed Acyclic Graph
<https://en.wikipedia.org/wiki/Directed_acyclic_graph>`__ (DAG ) of data and processing blocks [#]_.
It describes which data sources will be used, how the data will be processed and how these steps are connected.
One block can be used in multiple workflows.

.. figure:: _assets/workflow.png
    :align: center
    :scale: 35 %
    :alt: Workflow block diagram

    Example workflow with one data block and two cascaded processing blocks.

When constructing the workflow in the UP42 console, the connections between
blocks are evaluated using their :ref:`input and ouput capabilites <block-capabilities>`, specifying the resulting or demanded data type.
Only blocks with congruent capabilities can be attached to each other. **Data blocks** provide **only an ouput capability**, while
**processing block** provide **both an input and an ouput capability**.

.. _jobs-definition:

Jobs
====

A job is an instance of a workflow, run for a specified area of interest and parameter configuration.
The job page in the UP42 console shows the current **status** of the job, the **runtime**, **costs**
(broken down in data, processing and infrastructure costs), the **used parameters** and **job id**.
After the job is finished, the **job results can be downloaded** in this menu.

.. figure:: _assets/job_page.png
    :align: center
    :scale: 35 %
    :alt: Job overview page in the UP42 console

Each workflow block or step that was run in the job can be called **task**. For each job task, the **intermediate result can be downloaded** in
the task details page. Here we can also find the **log messages** of each task (used for e.g. error investigation and support).

Job parameters
--------------

In order to start a job, the user needs to specify the **job parameters**, consisting of:

* Data block :ref:`filters <filters>` (e.g. area of interest, time period etc.)
* Optional processing block **configuration** parameters (e.g. sharpening strength, filter size etc.)

.. _job-statuses:

Job statuses
------------

  + Before running the job:
      + ``not started``: the job/task hasn't started yet.
      + ``pending``: the job/task hasn't started yet but is pending to start.
    
  + While running:
      + ``running``: the job/task is running.
      + ``cancelling``: a request for cancelling the job has been issued, but the job is not **yet** cancelled.

  + After a job/task completed:
      + ``succeeded``: the job/task has finished successfully.
      + ``failed``: the job/task has failed.
      + ``cancelled``: the job/task as been cancelled.


.. rubric:: Footnotes

.. [#] Currently the workflow is a `linked list
       <https://en.wikipedia.org/wiki/Linked_list>`__
       of blocks, with a data
       block always at the root. Full DAG-based workflows will be
       implemented in the future.
