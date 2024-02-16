# RNP-PGId-2023
This is a public mirror of the repository https://git.rnp.br/ct-gid/pgid-2023/eap-5g

It contains the files resulting from the project in which I took part in

## Background

Some background information for the international visitors

Rede Nacional de Pesquisa (RNP) is a Brazilian research institution with international reach. One of its topics of research is the Identity Management (IdM), so there's Programa de Gestão de Identidades (PGId) which is a research program focused on IdM aspects that funds projects.

"Estudo e Avaliação de Métodos de Autenticação EAP na Infraestrutura de Redes de Telecomunicação 5G" is the title of the project that was selected* by RNP's 2023 PGId and it could be freely translated as "Evaluation Study of EAP Authentication Methods within 5G Networks"

\* Read the announcement [clicking here](https://www.rnp.br/noticias/projetos-escolhidos-para-o-programa-de-gestao-de-identidade-2023-sao-divulgados) (in Portuguese)

## Repository Description

At the root of the repository lie the files originating from the environment configured for testing the desired settings

The `.pcap` files contain packet captures taken during the tests by the free5gc instance. The `.tar.gz` and `.log` files contain logs from the components/NFs involved in the tests.

The authentication methods used by the UE (User Equipment) are indicated in the names of the corresponding files (5G-AKA and EAP-AKA).

The eap-aka-prime files attempt to showcase the issues encountered when using this authentication method between UERANSIM and free5gc. The `no-fix` suffix denotes files generated from the source code available in the official repository of the UERANSIM project. On the other hand, the `partial-fix` suffix presents an attempt to correct the interpretation of the signaling used by UERANSIM, which was based on the instructions contained in [an issue in the official repository](https://github.com/aligungr/UERANSIM/issues/592) of UERANSIM. The source code is available [via this link](https://github.com/oliveiraleo/UERANSIM/tree/aka-prime-PGId-2023).

The files with `ueransim` prefix represent logs from the components of the UERANSIM solution when using the EAP-AKA' authentication method.

### Packet Capture Filtering

In addition to providing complete captures found in the base `.pcap` files, some filters have been applied for better visualization of the most relevant packets for the study:

- Filter 0: 

`pfcp || icmp || gtp`

This filter is the one suggested by free5gc's [official documentation](https://free5gc.org/guide/4-test-free5gc/).

- Filter 1:

`!(ip.addr == 10.9.0.2 || ip.addr == 10.112.25.252/8 || arp || icmpv6 || ntp || browser)`

The IPs 10.9.0.2 and the range 10.x.x.x were removed because they were the IP used for remote accessing the virtual environment (via SSH) and the Mikrotik router that connected the physical server to the internet, respectively. The remaining protocols were filtered out as they were not the focus of the study.

**NOTE:** In order to be able to open the package content, setup Wireshark according to the [picture here](./docs/wireshark-decode-config-5g-aka.png).

### Instruction Manual

With a focus on research reproducibility, a instruction manual was created as part of the results of this research. It's writen in Portuguese and contains technical details of the testing environment used during the project. This manual can be found [inside the *docs* folder](./docs/Manual_de_Instrucoes_Core_5G.pdf).

**NOTE:** For the most up to date English instructions on how to setup the free5gc, please refer to their [official online manual page](https://free5gc.org/guide/).

## Useful URLs

- [free5gc](https://free5gc.org/)
- [UERANSIM](https://github.com/aligungr/UERANSIM)
- [Wireshark](https://www.wireshark.org/)

## Publications

To be added

## Acknowledgements

I'd like to acknowledge [Dr. Edelberto Franco Silva](https://sites.google.com/a/ice.ufjf.br/edelbertofranco/) my advisor on this project. I'd like to acknowledge the [Networks and Distributed Systems Laboratory](http://netlab.ice.ufjf.br/) (NetLab) of the [Federal University of Juiz de Fora](https://ufjf.br/) (UFJF) for providing the infrastructure used to carry on the experiments of this research. I'd like to acknowledge also [Coordenação de Aperfeicoamento de Pessoal de Nível Superior](https://www.gov.br/capes/) (CAPES) and [Rede Nacional de Pesquisa](https://www.rnp.br/) (RNP), institutions of the Ministry of Education and Ministry of Science, Technology and Innovation of the Brazillian Federal Government, respectively, for funding this research project.
