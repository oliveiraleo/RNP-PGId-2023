# RNP-PGId-2023

This is a public mirror of the repository at https://git.rnp.br/ct-gid/pgid-2023/eap-5g, which contains files resulting from the project in which I participated.

## Background Information

For international visitors:

Rede Nacional de Pesquisa (RNP) is a Brazilian research institution with international reach, focusing on topics such as Identity Management (IdM). The Programa de Gestão de Identidades (PGId) is a research program that funds projects related to IdM.

The project "Estudo e Avaliação de Métodos de Autenticação EAP na Infraestrutura de Redes de Telecomunicação 5G" (Evaluation Study of EAP Authentication Methods within 5G Networks) was selected by RNP's 2023 PGId. For more information, please visit [this announcement](https://www.rnp.br/noticias/projetos-escolhidos-para-o-programa-de-gestao-de-identidade-2023-sao-divulgados) (in Portuguese).

## Repository Description

This repository contains files originating from the testing environment, configured to evaluate specific settings.

The `.pcap` files contain packet captures taken during testing with the free5gc instance. The `.tar.gz` and `.log` files contain logs from the components (NFs) involved in the tests.

The authentication methods used by the User Equipment (UE) are indicated in the file names (5G-AKA and EAP-AKA).

The `eap-aka-prime` files demonstrate the issues encountered when using this authentication method between UERANSIM and free5gc. The `no-fix` suffix refers to files generated from the official UERANSIM project repository. The `partial-fix` suffix shows an attempt to correct the signaling interpretation used by UERANSIM, based on instructions in [Issue #592](https://github.com/aligungr/UERANSIM/issues/592). The source code is available at [this link](https://github.com/oliveiraleo/UERANSIM/tree/aka-prime-PGId-2023).

Files with the `ueransim` prefix represent logs from the UERANSIM components when using the EAP-AKA' authentication method.

### Packet Capture Filtering

In addition to the complete packet captures in the base `.pcap` files, filters have been applied to improve visualization of the most relevant packets for the study:

- Filter 0: 

`pfcp || icmp || gtp`

The filter used is based on the recommendation in free5gc's [official documentation](https://free5gc.org/guide/4-test-free5gc/).

- Filter 1:

`!(ip.addr == 10.9.0.2 || ip.addr == 10.112.25.252/8 || arp || icmpv6 || ntp || browser)`

To enhance clarity, the IPs 10.9.0.2 and the range 10.x.x.x were removed, as they were used for remote access to the virtual environment and the Mikrotik router, respectively. The remaining protocols were filtered out, as they were not the focus of the study.

**NOTE:** To access the package contents, follow the Wireshark setup instructions depicted in [this image](./docs/wireshark-decode-config-5g-aka.png).

### Instruction Manual

A research reproducibility guide has been created as part of the project's results. The manual, written in Portuguese, provides technical details on the testing environment used during the project. The manual can be accessed [here](./docs/Manual_de_Instrucoes_Core_5G.pdf).

**NOTE:** For the most up-to-date English instructions on setting up free5GC, please refer to their [official online manual page](https://free5gc.org/guide/).

## Useful URLs

- [free5gc](https://free5gc.org/)
- [UERANSIM](https://github.com/aligungr/UERANSIM)
- [Wireshark](https://www.wireshark.org/)

## Publications

Please, cite this work as:

L. Oliveira and E. Silva. " Estudo e Avaliação de Métodos de Autenticação EAP na Infraestrutura de Redes de Telecomunicação 5G", in *Anais Estendidos do XXIII Simpósio Brasileiro de Segurança da Informação e de Sistemas Computacionais*, Juiz de Fora/MG, 2023, pp. 97-100, doi: https://doi.org/10.5753/sbseg_estendido.2023.235845.

Or use the BibTex code below:
```
@inproceedings{sbseg_estendido_EAP,
 author = {Leonardo Oliveira and Edelberto Silva},
 title = {Estudo e Avaliação de Métodos de Autenticação EAP na Infraestrutura de Redes de Telecomunicação 5G},
 booktitle = {Anais Estendidos do XXIII Simpósio Brasileiro de Segurança da Informação e de Sistemas Computacionais},
 location = {Juiz de Fora/MG},
 year = {2023},
 pages = {97--100},
 publisher = {SBC},
 address = {Porto Alegre, RS, Brasil},
 doi = {10.5753/sbseg_estendido.2023.235845},
 url = {https://sol.sbc.org.br/index.php/sbseg_estendido/article/view/27280}
}
```

## Acknowledgements

I'd like to acknowledge [Dr. Edelberto Franco Silva](https://sites.google.com/a/ice.ufjf.br/edelbertofranco/) my advisor on this project. I'd like to acknowledge the [Networks and Distributed Systems Laboratory](http://netlab.ice.ufjf.br/) (NetLab) of the [Federal University of Juiz de Fora](https://ufjf.br/) (UFJF) for providing the infrastructure used to carry on the experiments of this research. I'd like to acknowledge also [Coordenação de Aperfeicoamento de Pessoal de Nível Superior](https://www.gov.br/capes/) (CAPES) and [Rede Nacional de Pesquisa](https://www.rnp.br/) (RNP), institutions of the [Ministry of Education](https://en.wikipedia.org/wiki/Ministry_of_Education_(Brazil)) (MEC) and [Ministry of Science, Technology and Innovation](https://en.wikipedia.org/wiki/Ministry_of_Science,_Technology_and_Innovation_(Brazil)) (MCTI) of the Federal Government of Brazil, respectively, for funding this research project.
