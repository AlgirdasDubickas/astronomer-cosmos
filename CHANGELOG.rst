Changelog
=========

1.3.2 (2023-01-26)
------------------

Bug fixes

* Fix: ensure ``DbtGraph.update_node_dependency`` is called for all load methods by @jbandoro in #803
* Fix: ensure operator ``execute`` method is consistent across all execution base subclasses by @jbandoro in #805
* Fix custom selector when ``test`` node has no ``depends_on`` values by @tatiana in #814
* Fix forwarding selectors to test task when using ``TestBehavior.AFTER_ALL`` by @tatiana in #816

Others

* Docs: Remove incorrect docstring from ``DbtLocalBaseOperator`` by @jakob-hvitnov-telia in #797
* Add more logs to troubleshoot custom selector by @tatiana in #809
* Fix OpenLineage integration documentation by @tatiana in #810
* Fix test dependencies after Airflow 2.8 release by @jbandoro and @tatiana in #806
* Use Airflow constraint file for test environment setup by @jbandoro in #812
* pre-commit updates in #799, #807


1.3.1 (2023-01-10)
------------------

Bug fixes

* Fix disable event tracking throwing error by @jbandoro in #784
* Fix support for string path for ``LoadMode.DBT_LS_FILE`` and docs by @flinz in #788
* Remove stack trace to disable unnecessary K8s error by @tatiana in #790

Others

* Update examples to use the astro-runtime 10.0.0 by @RNHTTR in #777
* Docs: add missing imports for mwaa getting started by @Benjamin0313 in #792
* Refactor common executor constructors with test coverage by @jbandoro in #774
* pre-commit updates in #789


1.3.0 (2023-01-04)
------------------

Features

* Add new parsing method ``LoadMode.DBT_LS_FILE`` by @woogakoki in #733 (`documentation <https://astronomer.github.io/astronomer-cosmos/configuration/parsing-methods.html#dbt-ls-file>`_).
* Add support to select using (some) graph operators when using ``LoadMode.CUSTOM`` and ``LoadMode.DBT_MANIFEST`` by @tatiana in #728 (`documentation <https://astronomer.github.io/astronomer-cosmos/configuration/selecting-excluding.html#using-select-and-exclude>`_)
* Add support for dbt ``selector`` arg for DAG parsing by @jbandoro in #755 (`documentation <https://astronomer.github.io/astronomer-cosmos/configuration/render-config.html#render-config>`_).
* Add ``ProfileMapping`` for Vertica by @perttus in #540, #688 and #741 (`documentation <https://astronomer.github.io/astronomer-cosmos/profiles/VerticaUserPassword.html>`_).
* Add ``ProfileMapping`` for Snowflake encrypted private key path by @ivanstillfront in #608 (`documentation <https://astronomer.github.io/astronomer-cosmos/profiles/SnowflakeEncryptedPrivateKeyFilePem.html>`_).
* Add support for Snowflake encrypted private key environment variable by @DanMawdsleyBA in #649
* Add ``DbtDocsGCSOperator`` for uploading dbt docs to GCS by @jbandoro in #616, (`documentation <https://astronomer.github.io/astronomer-cosmos/configuration/generating-docs.html#upload-to-gcs>`_).
* Add cosmos/propagate_logs Airflow config support for disabling log propagation by @agreenburg in #648 (`documentation <https://astronomer.github.io/astronomer-cosmos/configuration/logging.html>`_).
* Add operator_args ``full_refresh`` as a templated field by @joppevos in #623
* Expose environment variables and dbt variables in ``ProjectConfig`` by @jbandoro in #735 (`documentation <https://astronomer.github.io/astronomer-cosmos/configuration/project-config.html#project-config-example>`_).
* Support disabling event tracking when using Cosmos profile mapping by @jbandoro in #768 (`documentation <https://astronomer.github.io/astronomer-cosmos/profiles/index.html#disabling-dbt-event-tracking>`_).

Enhancements

* Make Pydantic an optional dependency by @pixie79 in #736
* Create a symbolic link to ``dbt_packages`` when ``dbt_deps`` is False when using ``LoadMode.DBT_LS`` by @DanMawdsleyBA in #730
* Add ``aws_session_token`` for Athena mapping by @benjamin-awd in #663
* Retrieve temporary credentials from ``conn_id`` for Athena by @octiva in #758
* Extend ``DbtDocsLocalOperator`` with static flag by @joppevos  in #759

Bug fixes

* Remove Pydantic upper version restriction so Cosmos can be used with Airflow 2.8 by @jlaneve in #772

Others

* Replace flake8 for Ruff by @joppevos in #743
* Reduce code complexity to 8 by @joppevos in #738
* Speed up integration tests by @jbandoro in #732
* Fix README quickstart link in by @RNHTTR in #776
* Add package location to work with hatchling 1.19.0 by @jbandoro in #761
* Fix type check error in ``DbtKubernetesBaseOperator.build_env_args`` by @jbandoro in #766
* Improve ``DBT_MANIFEST`` documentation by @dwreeves in #757
* Update conflict matrix between Airflow and dbt versions by @tatiana in #731 and #779
* pre-commit updates in #775, #770, #762


1.2.5 (2023-11-23)
------------------

Bug fixes

* Fix running models that use alias while supporting dbt versions by @binhnq94 in #662
* Make ``profiles_yml_path`` optional for ``ExecutionMode.DOCKER`` and ``KUBERNETES`` by @MrBones757 in #681
* Prevent overriding dbt profile fields with profile args of "type" or "method" by @jbandoro in #702
* Fix ``LoadMode.DBT_LS`` fail when dbt outputs ``WarnErrorOptions`` by @adammarples in #692
* Add support for env vars in ``RenderConfig`` for dbt ls parsing by @jbandoro in #690
* Add support for Kubernetes ``on_warning_callback`` by @david-mag in #673
* Fix ``ExecutionConfig.dbt_executable_path`` to use ``default_factory`` by @jbandoro in #678

Others

* Docs fix: example DAG in the README and docs/index by @tatiana in #705
* Docs improvement: highlight DAG examples in README by @iancmoritz and @jlaneve in #695


1.2.4 (2023-11-14)
------------------

Bug fixes

* Store ``compiled_sql`` even when task fails by @agreenburg in #671
* Refactor ``LoadMethod.LOCAL`` to use symlinks instead of copying directory by @jbandoro in #660
* Fix 'Unable to find the dbt executable: dbt' error by @tatiana in #666
* Fix installing deps when using ``profile_mapping`` & ``ExecutionMode.LOCAL`` by @joppevos in #659

Others

* Docs: add execution config to MWAA code example by @ugmuka in #674
* Docs: highlight DAG examples in docs by @iancmoritz and @jlaneve in #695


1.2.3 (2023-11-09)
------------------

Bug fix

* Fix reusing config across TaskGroups/DAGs by @tatiana in #664


1.2.2 (2023-11-06)
------------------

Bug fixes

* Support ``ProjectConfig.dbt_project_path = None`` & different paths for Rendering and Execution by @MrBones757 in #634
* Fix adding test nodes to DAGs built using ``LoadMethod.DBT_MANIFEST`` and ``LoadMethod.CUSTOM`` by @edgga in #615

Others

* Add pre-commit hook for McCabe max complexity check and fix errors by @jbandoro in #629
* Update contributing docs for running integration tests by @jbandoro in #638
* Fix CI issue running integration tests by @tatiana in #640 and #644
* pre-commit updates in #637


1.2.1 (2023-10-25)
------------------

Bug fixes

* Resolve errors occurring when ``dbt_project_path`` is str and partial support ``dbt_project_path=None`` by @MrBones757 in #605
* Fix running dbt tests that depend on multiple models (support ``--indirect-selection buildable``) by @david-mag in #613
* Add tests to sources, snapshots and seeds when using ``TestBehavior.AFTER_EACH`` by @tatiana in #599
* Fix custom selector when select has a subset of tags of the models' tags by @david-mag in #606
* Fix ``LoadMode.AUTOMATIC`` behaviour to use ``LoadMode.DBT_LS`` when ``ProfileMapping`` is used by @tatiana in #625
* Fix failure if ``openlineage-common`` raises a jinja exception by @tatiana in #626

Others

* Update contributing guide docs by @raffifu in #591
* Remove unnecessary stack trace from Cosmos initialization by @tatiana in #624
* Fix running test that validates manifest-based DAGs by @tatiana in #619
* pre-commit updates in #604 and #621


1.2.0 (2023-10-13)
------------------

Features

* Add support to model versioning available since dbt 1.6 by @binhnq94 in #516
* Add AWS Athena profile mapping by @benjamin-awd in #578
* Support customizing how dbt nodes are converted to Airflow by @tatiana in #503
* Make the arg ``dbt_project_path`` in the ``ProjectConfig`` optional by @MrBones757 in #581

Bug fixes

* Fix Cosmos custom selector to support filtering a single model by @jlaneve and @harels in #576
* Fix using ``GoogleCloudServiceAccountDictProfileMapping`` together with ``LoadMethod.DBT_LS`` by @joppevos in #587
* Fix using the ``full_refresh`` argument in projects that contain tests by @EgorSemenov and @tatiana in #590
* Stop creating symbolic links for ``dbt_packages`` (solves ``LocalExecutor`` concurrency issue) by @tatiana in #600

Others

* Docs: add reference to original Jaffle Shop project by @erdos2n in #583
* Docs: retries & note about DagBag error by @TJaniF in #592
* pre-commit updates in #575 and #585


1.1.3 (2023-09-28)
------------------

Bug fixes

* Only create task group and test task only if the model has a test by @raffifu in #543
* Fix parsing test nodes when using the custom load method (LoadMethod.CUSTOM) by @raffifu in #563
* Fix ``DbtTestOperator`` when test does not have ``test_metadata`` by @javihernovoa and @tatiana in #565
* Support dbt 1.6 and apache-airflow-providers-cncf-kubernetes 7.3.0  by @tatiana in #564



1.1.2 (2023-09-27)
------------------

Bug fixes

* Fix using ``ExecutionMode.KUBERNETES`` by @pgoslatara and @tatiana in #554
* Add support to ``apache-airflow-providers-cncf-kubernetes < 7.4.0`` by @tatiana in #553
* Fix ``on_warning_callback`` behaviour on ``DbtTestLocalOperator`` by @edgga, @marco9663 and @tatiana in #558
* Use ``returncode`` instead of ``stderr`` to determine dbt graph loading errors by @cliff-lau-cloverhealth in #547
* Improve error message in ``config.py`` by @meyobagero in #532
* Fix ``DbtTestOperator`` when test does not have ``test_metadata`` by @tatiana in #558
* Fix ``target-path`` not specified issue in ``dbt-project.yml`` by @tatiana in #533

Others

* Docs: add reference links to dbt and Airflow columns by @TJaniF in #542
* pre-commit updates #552 and #546



1.1.1 (2023-09-14)
------------------

Bug fixes

* Fix attempt of emitting OpenLineage events if task execution fails by @tatiana in #526
* Fix Rust dependency for Windows users by @tatiana in #526
* Fix DbtRunOperationLocalOperator missing flags by @tatiana in #529
* Fix DbtRunLocalOperator to support the full refresh argument by @tatiana in #529
* Remove redundant prefix of task names when test_behavior = TestBehavior.AFTER_EACH by @binhnq94 in #524
* Fix rendering vars in ``DbtModel`` when using ``LoadMode.CUSTOM`` by @dojinkimm in #502

Others

* Docs: add `documentation comparing Airflow and dbt concepts <https://astronomer.github.io/astronomer-cosmos/getting_started/dbt-airflow-concepts.html>`_ by @tatiana in #523.
* Update PyPI project links by @tatiana in #528
* pre-commit updates


1.1.0 (2023-09-06)
------------------

Features

* Support dbt global flags (via dbt_cmd_global_flags in operator_args) by @tatiana in #469
* Support parsing DAGs when there are no connections by @jlaneve in #489

Enhancements

* Hide sensitive field when using BigQuery keyfile_dict profile mapping by @jbandoro in #471
* Consistent Airflow Dataset URIs, inlets and outlets with `Openlineage package <https://pypi.org/project/openlineage-integration-common/>`_ by @tatiana in #485. `Read more <https://astronomer.github.io/astronomer-cosmos/configuration/lineage.html>`_.
* Refactor ``LoadMethod.DBT_LS`` to run from a temporary directory with symbolic links by @tatiana in #488
* Run ``dbt deps`` when using ``LoadMethod.DBT_LS`` by @DanMawdsleyBA in #481
* Update Cosmos log color to purple by @harels in #494
* Change operators to log ``dbt`` commands output as opposed to recording to XCom by @tatiana in #513

Bug fixes

* Fix bug on select node add exclude selector subset ids logic by @jensenity in #463
* Refactor dbt ls to run from a temporary directory, to avoid Read-only file system errors during DAG parsing, by @tatiana in #414
* Fix profile_config arg in DbtKubernetesBaseOperator by @david-mag in #505
* Fix SnowflakePrivateKeyPemProfileMapping private_key reference by @nacpacheco in #501
* Fix incorrect temporary directory creation in VirtualenvOperator init by @tatiana in #500
* Fix log propagation issue by @tatiana in #498
* Fix PostgresUserPasswordProfileMapping to retrieve port from connection by @jlneve in #511

Others

* Docs: Fix RenderConfig load argument by @jbandoro in #466
* Enable CI integration tests from external forks by @tatiana in #458
* Improve CI tests runtime by @tatiana in #457
* Change CI to run coverage after tests pass by @tatiana in #461
* Fix forks code revision in code coverage by @tatiana in #472
* [pre-commit.ci] pre-commit autoupdate by @pre-commit-ci in #467
* Drop support to Python 3.7 in the CI test matrix by @harels in #490
* Add Airflow 2.7 to the CI test matrix by @tatiana in #487
* Add MyPy type checks to CI since we exceeded pre-commit disk quota usage by @tatiana in #510

1.0.5 (2023-08-09)
------------------

Enhancements

* Improve logs to include astornomer-cosmos identifier by @tatiana in #450
* Support OAuth authentication for Big Query by @MonideepDe in #431

Bug fixes

* Fix selector for config tags by @javihernovoa in #441
* Fix BigQuery keyfile_dict mapping for connection created from webserver UI by @jbandoro in #449

Others

* [pre-commit.ci] pre-commit autoupdate by @pre-commit-ci in #446
* Resolve MyPy errors when adding Airflow pre-commit dependency by @abhi12mohan in #434


1.0.0 (2022-12-14)
-------------------

* Initial release, with the following **6** workflow Operators/Parsers:

.. list-table::
   :header-rows: 1

   * - Operator/Sensor Class
     - Import Path
     - Example DAG

   * - ``DBTTestOperator``
     - .. code-block:: python

        from cosmos.providers.dbt.core.operators import DBTBaseOperator
     - N/A

   * - ``DBTSeedOperator``
     - .. code-block:: python

        from cosmos.providers.dbt.core.operators import DBTSeedOperator
     - `Example DAG <https://github.com/astronomer/astronomer-cosmos/blob/1.0.0/examples/dags/extract_dag.py>`__

   * - ``DBTRunOperator``
     - .. code-block:: python

        from cosmos.providers.dbt.core.operators import DBTRunOperator
     - N/A

   * - ``DBTTestOperator``
     - .. code-block:: python

        from cosmos.providers.dbt.core.operators import DBTTestOperator
     - N/A

   * - ``DbtDag``
     - .. code-block:: python

        from cosmos.providers.dbt.core.dag import DbtDag
     - `Example DAG <https://github.com/astronomer/astronomer-cosmos/blob/1.0.0/examples/dags/attribution-playbook.py>`__

   * - ``DbtTaskGroup``
     - .. code-block:: python

        from cosmos.providers.dbt.core.dag import DbtTaskGroup
     - `Example DAG <https://github.com/astronomer/astronomer-cosmos/blob/1.0.0/examples/dags/jaffle_shop.py>`__
