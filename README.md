# TP23-24 – Laravel.io Deployment with Kubernetes & Ansible

Este repositório contém o código-fonte e os ficheiros auxiliares desenvolvidos no âmbito do projeto da Unidade Curricular de **Aplicações e Serviços de Computação em Nuvem** (Ano Letivo 2023/2024) do **Mestrado em Engenharia Informática da Universidade do Minho**.

## Estrutura do Repositório

- [`codebase`](codebase): Contém os **Playbooks Ansible** e ficheiros de suporte usados na instalação e gestão da infraestrutura e da aplicação Laravel.io.
- [`ASCN-TP-Grupo41-Report.pdf`](ASCN-TP-Grupo41-Report.pdf): Relatório técnico detalhado com descrição da arquitetura, testes, resultados e conclusões.

## 🎯 Objetivo do Projeto

Automatizar o processo de instalação e configuração da aplicação **[Laravel.io](https://laravel.io)** na **Google Cloud Platform (GCP)**, utilizando:

- **Google Kubernetes Engine (GKE)** para orquestração de serviços;
- **Google Cloud SQL** para persistência de dados;
- **Google Compute Engine (GCE)** para automação de tarefas;
- **Ansible** para automatizar o ciclo de vida da infraestrutura;
- **Google Cloud Monitoring** e **Apache JMeter** para monitorização e testes de desempenho.

## Arquitetura da Solução

A arquitetura proposta foca-se na **escalabilidade**, **resiliência** e **simplicidade de acesso**:

- **Pods Laravel.io** que encapsulam a aplicação com PHP e dependências;
- **Serviço MySQL** com PVC (Persistent Volume Claim) para garantir a persistência dos dados;
- **NodePort Service** para expor a aplicação externamente;
- **Horizontal Pod Autoscaler (HPA)** para escalar automaticamente os pods conforme a carga do sistema.

## Tecnologias Utilizadas

- **Ansible**
- **Docker**
- **Kubernetes (GKE)**
- **Google Cloud SQL**
- **Google Compute Engine (GCE)**
- **Google Cloud Monitoring**
- **Apache JMeter**

## Testes e Resultados

Foram realizados testes de carga utilizando o **Apache JMeter**, simulando 1000 pedidos simultâneos do tipo HTTP GET à aplicação.

### Resultados observados:
- Após a implementação do **HPA**, a utilização de memória foi controlada (máx. 98%);
- A média de resposta aos pedidos foi de apenas **27 ms**;
- A aplicação mostrou-se **resiliente** e **estável**, com escalabilidade automática eficiente.

Mais detalhes disponíveis no relatório anexo.

## Conclusão

O projeto demonstra uma solução moderna, automatizada e escalável para a implementação de aplicações web em cloud. O uso do Kubernetes em conjunto com Ansible e ferramentas de monitorização garante uma gestão eficiente e adaptável às cargas de trabalho.

## Trabalho Futuro

- Otimização da gestão de memória da aplicação;
- Substituição do NodePort por um **Ingress Controller** para uma gestão de tráfego mais avançada;
- Implementação de **backups automáticos**;
- Testes de desempenho mais diversificados e contínuos.

---

**Grupo 41 – Universidade do Minho**  
André Nunes · Afonso Cruz · Beatriz Rocha · Catarina Martins · Duarte Serrão
