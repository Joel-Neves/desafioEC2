# desafioEC2

# Laboratório: Gerenciamento de Instâncias EC2 na AWS

## Objetivo
Este repositório é o entregável de um laboratório prático focado em consolidar conhecimentos em gerenciamento de instâncias EC2 na AWS. O material aqui organizado contém as anotações, o desenho arquitetural e os insights adquiridos durante a prática, servindo como base de apoio para estudos e futuras implementações.

## Contexto da Prática: Arquitetura de E-commerce
Para tangibilizar o uso do EC2, foi desenhada uma arquitetura básica de e-commerce, mapeando como o servidor de aplicação se comunica com os demais serviços da nuvem.

A estrutura foi dividida da seguinte forma:
*   Backend (EC2 com Spring Boot): O núcleo da prática. A instância computacional que processa as regras de negócio.
*   Frontend (Aplicação Web): A interface do usuário.
*   CDN & Storage (CloudFront + S3): Camada de entrega de conteúdo estático (imagens).
*   Balanceamento (ALB): O Application Load Balancer roteando requisições dinâmicas para o EC2.
*   Banco de Dados (RDS PostgreSQL): Serviço gerenciado para armazenamento relacional.

## Anotações e Insights
Durante o desenho e revisão da arquitetura, alguns conceitos críticos de infraestrutura ficaram claros:
1.  Sobrecarga Desnecessária no EC2: Passar conteúdo estático (fotos de produtos) pelo servidor de aplicação é um erro de design. Esses arquivos devem ser roteados diretamente do S3 pela CDN (CloudFront), poupando banda e processamento do EC2.
2.  Uso Correto do Load Balancer: O ALB existe para distribuir tráfego de requisições lógicas entre as instâncias EC2. Ele não tem função no roteamento de cache ou ativos estáticos.
