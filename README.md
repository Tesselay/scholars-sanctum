<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a id="readme-top"></a>



<!-- PROJECT SHIELDS -->
[![Commits][commits-shield]][commits-url]
[![Last Commit][last-commit-shield]][last-commit-url]
[![Issues][issues-shield]][issues-url]
[![Unlicense License][license-shield]][license-url]



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
    <li><a href="#faq">FAQ</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

*Scholar's Sanctum* is my home lab project named by my vastly unfinished personal tool suite.

This is an Ansible project which will be run on a freshly installed proxmox host to bootstrap basic configuration, including:
* Setting up admin users on host & datacenter
* Configuring SSH on host
* Configuring repositories
* Generating a base debian vm template

For admins and the template I provided variables so the roles can be configured as desired. It is still rather basic though.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Built With

![Ansible Badge](https://img.shields.io/badge/Ansible-EE0000?logo=ansible&logoColor=fff&style=for-the-badge)
![Proxmox Badge](https://img.shields.io/badge/Proxmox-EE5700?logo=proxmox&logoColor=fff&style=for-the-badge)
![Debian Badge](https://img.shields.io/badge/Debian-A81D33?logo=debian&logoColor=fff&style=for-the-badge)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

**1.** Setup SSH agent on client

Only really recommended when using a passphrase-protected ssh key so that you don't have to reenter it every time you run a play.
```shell
eval "$(ssh-agent -s)"
ssh-add <private-key-location>
```

**2.** Run playbooks
```shell
ansible-playbook bootstrap_proxmox.yml -i ./inventory/hosts.ini --ask-vault-pass
ansible-playbook configure_datacenter.yml -i ./inventory/hosts.ini --ask-vault-pass
```

### Prerequisites

* Linux or WSL
* Ansible installed on device
* Versions used
  * *Proxmox*: 8.4.1
  * *Ansible*: 2.14.18

### Installation

**1.** Install proxmox manually on server device.

**2.** Reset root password to something more secure, if not already done so.
* Change on datacenter through GUI
* Change on host using `passwd`

**3.** Configure storage.

**4.** Generate SSH key on client
```shell
ssh-keygen
```

**4.** Provide client ssh key to root
```shell
ssh-copy-id -i <public-key-location> root@<host>
```

### Configuration

**1.** Generate vault file with secrets and the following structure
```shell
ansible-vault create group_vars/sanctum/vault.yml
```
```yml
vault_admins:
  <name>: "<password-hash>"
ansible_become_password: "<password>"
ansible_ssh_private_key_file: "<private-key-location>"
```

Alternatively omit `ansible_become_password` and provide `ask-become-pass` ad-hoc when running the playbook.

**2.** Configure `group_vars/sanctum/settings.yml` and `proxmox_template` as desired

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

* [ ] Configure storage per Ansible
* [ ] Add role argument validation



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



<!-- LICENSE -->
## License

Distributed under the GNU GPLv3. See `LICENSE.md` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [Ansible Community Documentation](https://docs.ansible.com/ansible/latest/index.html)
* [RedHat Automation Blog](https://www.redhat.com/en/blog/channel/management-and-automation)
* [Proxmox Documentation](https://pve.proxmox.com/pve-docs/)
* [Ansible Lint](https://ansible.readthedocs.io/projects/lint/)


* [Best README template](https://github.com/othneildrew/Best-README-Template)
* [Choose an Open Source License](https://choosealicense.com)
* [Img Shields](https://shields.io)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- FAQ -->
## FAQ

### Why not use the community proxmox module?

I wanted the initialization to be as simple as possible. Also it's a great learning experience.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[commits-shield]: https://img.shields.io/github/commit-activity/t/Tesselay/scholars-sanctum
[commits-url]: https://github.com/Tesselay/scholars-sanctum/graphs/commit-activity
[last-commit-shield]: https://img.shields.io/github/last-commit/Tesselay/scholars-sanctum
[last-commit-url]: https://github.com/Tesselay/scholars-sanctum/graphs/commit-activity
[issues-shield]: https://img.shields.io/github/issues/Tesselay/scholars-sanctum
[issues-url]: https://github.com/Tesselay/scholars-sanctum/issues
[license-shield]: https://img.shields.io/github/license/Tesselay/scholars-sanctum
[license-url]: https://github.com/Tesselay/scholars-sanctum/blob/master/LICENSE.md

[Angular.io]: https://img.shields.io/badge/Angular-%23DD0031.svg?logo=angular&logoColor=white
[Angular-url]: https://angular.io/
[Docker.io]: https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=fff
[Docker-url]: https://www.docker.com/