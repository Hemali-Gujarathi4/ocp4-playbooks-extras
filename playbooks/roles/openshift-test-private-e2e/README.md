Validate openshift-test-private e2e
=========
This ansible playbook can be used to validate openshift-test-private e2e for filter testcases in openshift cluster.  


Requirements
------------

- Access to the cluster as a user with the cluster-admin role.
- The cluster is in a known good state, without any errors.
- OCP secret with name ***podman-secret*** in the default namespace which is used for global secret update and has following keys: ***username***, ***password*** and ***registry***


Role Variables
--------------

| Variable                                   | Required | Default                                                                              | Comments                                                                                                                       |
|--------------------------------------------|----------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| validate_otp                            | yes     | false                                                                                | Set it to true to run this playbook                                                                                            |
| openshift_test_private_directory                          | yes       | `/tmp/openshift_test_private_e2e`                                                                       | Working directory for openshift_test_private e2e  tests                                                                                         |
| openshift_test_private_golang_tarball                     | yes       | https://go.dev/dl/go1.24.1.linux-ppc64le.tar.gz                                      | HTTPS URL for golang tarball                                                                                                   |
| openshift_test_private_e2e_repo | yes      | https://github.com/openshift/openshift-tests-private.git                             | Github repository for openshift tests private                                                                                  |
| openshift_test_private_git_branch | yes      | master                                                                               | Git branch for the openshift repo                                                                                              |
| testcase_filters_enable | yes       | true                                                                 | Set this value true to run filtered single or multiple testcases e2e and Set value to false to run all the e2e testcases.                                                                                                  |
| testcase_filters | yes      | []                                                                  | Testcases that  need to be tested, should be given in list format as ['Image_Registry', 'PersistentVolumes']                                                                                                    |


Environment Variables
---------------------

| Variable             | Required       | Comments                                                                |
|----------------------|----------------|--------------------------------------------                             |
| GITHUB_USERNAME      | yes            | Public GitHub account username to which the repository access granted.  |
| GITHUB_ACCESS_TOKEN  | yes            | GitHub personal access token to clone the repository.                   |

Dependencies
------------

 - None
 
Example Playbook
----------------
```
- name: Validate openshift-test-private for filtered testcases and run e2e
  hosts: bastion
  roles:
  - openshift-test-private-e2e

```

Steps to run playbook
----------------------

 - Copy `ocp4-playbooks-extras/examples/inventory` file to the home or working directory and modify it to add a remote host
 - To execute the playbook run the below sample command

Sample Command
---------------

ansible-playbook -i inventory -e examples/openshift-test-private-e2e-vars.yaml ~/ocp4-playbooks-extras/playbooks/openshift-test-private-e2e.yml

License
-------

See LICENCE.txt

Author Information
------------------

Hemali.Gujarathi4@ibm.com
