# Sistema de Gestão de Consultas Médicas  
**Documentação Técnica Completa**

**Grupo de Arquitetura de Software**  
**Professora**: Angélica Guimarães  
**Curso**: Engenharia de Software – PUC Minas  

---

## 1. Contexto do Sistema

### 1.1. Objetivos

Modernizar o sistema de gestão da clínica Vida+ Saúde, substituindo processos manuais por:

- Agendamento online por pacientes  
- Visualização em tempo real da agenda por médicos  
- Dashboard administrativo com métricas de atendimento  

### 1.2. Requisitos Arquiteturais

| Requisito        | Solução Adotada         | Justificativa                               |
|------------------|-------------------------|---------------------------------------------|
| Escalabilidade   | Microserviços           | Preparado para expansão futura              |
| Segurança        | Spring Security + JWT   | Autenticação robusta                        |
| Responsividade   | Design System + Tailwind CSS | Adaptação a dispositivos móveis      |
| Manutenibilidade | React + Storybook       | Componentização e documentação clara        |

---

## 2. Fluxos de Processo

### 2.1. Fluxograma de Agendamento



---

## 3. Design System Detalhado

### 3.1. Fundamentos Visuais

#### Paleta de Cores

- **Primária** (#007968 - Verde Água Escuro)  
  Transmite tranquilidade e confiança. Usada em botões primários e cabeçalhos.

- **Secundária** (#88C9D5 - Azul Claro)  
  Remete a limpeza e profissionalismo. Usada em botões secundários e interações.

- **Apoio** (#FF5252 - Vermelho)  
  Utilizada para mensagens de erro e alertas. Representa urgência e destaque.

- **Neutra** (#E0E0E0 - Cinza Claro)  
  Utilizada em fundos, bordas e estados desabilitados. Facilita leitura e reduz fadiga visual.

#### Tipografia

- **Títulos**: Roboto Condensed (700)  
  - Tamanhos: 2.5rem (h1), 2rem (h2)

- **Corpo do Texto**: Open Sans (400)  
  - Base: 1rem  
  - Legendas: 0.875rem  

#### Estados de Botões

| Estado       | Cor        |
|--------------|------------|
| Normal       | #88C9D5    |
| Hover        | #00796B    |
| Desabilitado | #E0E0E0    |

#### Tokens de Espaçamento

| Token        | Valor | Uso                              |
|--------------|-------|-----------------------------------|
| --space-xs   | 4px   | Espaçamentos internos pequenos    |
| --space-md   | 16px  | Padding padrão                    |
| --space-lg   | 24px  | Margens entre seções              |

---

## 4. Arquitetura do Sistema

### 4.1. Diagrama de 3 Camadas

#### Frontend (React.js)

- Tecnologias: React, Redux, Tailwind CSS, Storybook  
- Comunicação com backend via API REST  
- Gerenciamento de estado com Redux  

#### Backend (Spring Boot)

- Tecnologias: Spring Security + JWT, API REST, PostgreSQL, MongoDB  
- Padrões: Repository, Strategy  

#### Banco de Dados

- **PostgreSQL**: Dados relacionais  
- **MongoDB**: Logs e histórico de consultas (CQRS)

#### Ligações entre Camadas

- **Frontend ↔ Backend**: Requisições HTTP com autenticação via JWT  
- **Backend ↔ Banco de Dados**: JDBC (PostgreSQL) e drivers nativos (MongoDB)

#### Decisões Críticas (ADRs)

- **Spring Boot**: Ideal para regras complexas e integração com JPA  
- **Microserviços**: Facilitam escalabilidade e separação de módulos  

#### Resumo das Qualidades Arquiteturais

- Escalabilidade: Microserviços  
- Segurança: JWT + RBAC  
- Desempenho: Cache de consultas  
- Manutenibilidade: Componentes React documentados com Storybook  

### 4.2. Decisões Arquiteturais

| Camada         | Tecnologia            | Benefícios                                 |
|----------------|-----------------------|---------------------------------------------|
| Apresentação   | React                 | Estado global e componentes reutilizáveis   |
| Negócio        | Spring Boot (Java)    | Suporte a regras de negócio complexas       |
| Dados          | PostgreSQL + MongoDB  | ACID + flexibilidade para dados não estruturados |

### 4.3. Padrões e Estilos Arquiteturais

#### Estilo Arquitetural Principal

- **Padrão**: Arquitetura em Camadas (3-Tier)  
- **Justificativa**:  
  - Separação clara de responsabilidades  
  - Facilita manutenção e escalabilidade vertical

#### Padrões Complementares

| Padrão      | Aplicação no Sistema     | Benefício                              |
|-------------|---------------------------|----------------------------------------|
| MVC         | Frontend (React)          | Separação entre View e Controller      |
| Repository  | Backend (Spring Boot)     | Isola acesso ao banco de dados         |
| Strategy    | Validação de regras       | Flexibilidade para alterações           |

### 4.4. Decisões Arquiteturais Críticas (ADRs)

- **ADR-001**: Uso do Spring Boot  
  - Contexto: Validação de regras como cancelamento com 24h de antecedência  
  - Alternativas: Node.js (Express), Python (Django)  
  - Consequências: Integração simplificada com JPA e Spring Security  

- **ADR-002**: Uso do MongoDB para Logs  
  - Contexto: Armazenamento de dados não estruturados (ex: histórico de consultas)  
  - Padrão: CQRS (Command Query Responsibility Segregation)  

### 4.5. Qualidades Arquiteturais Atendidas

| Atributo       | Como é Garantido                        |
|----------------|------------------------------------------|
| Escalabilidade | Arquitetura baseada em microserviços     |
| Segurança      | JWT + Spring Security + RBAC             |
| Desempenho     | Cache de consultas mais acessadas        |
| Testabilidade  | Componentes React isolados no Storybook  |

---

## 5. Modelagem de Dados Avançada

### 5.1. DER Completo

> *(Diagrama visual não incluído nesta versão textual)*

---

## 6. Plano de Testes

### 6.1. Matriz de Testes

| Tipo         | Ferramenta | Cobertura                          |
|--------------|------------|-------------------------------------|
| Unitário     | Jest       | 85%+ dos componentes React          |
| Integração   | Postman    | 100% dos endpoints da API           |
| UI           | Cypress    | Telas críticas e principais fluxos  |
