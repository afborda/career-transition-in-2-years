## Data Science Roadmap - Papai Edition

Este repositório contém uma página estática (`index.html`) que apresenta um roadmap de 24 meses para transição de carreira Mobile Dev → Data Scientist, adaptado para pais de recém-nascidos.

### Objetivo

- Apresentar um plano de estudo prático, dividido em trimestres, com cursos, certificações e ferramentas sugeridas.
- Oferecer apoio motivacional e dicas específicas para pais (micro-estudos, organização, sono, etc.).
- Fornecer uma calculadora simples de ROI para estimar retorno financeiro da transição.

### Arquivos

- `index.html` — página única com todo o HTML, CSS e JavaScript embutidos. (UI, animações, lógica de cálculo e persistência local)

### Estrutura e seções principais

- Header: título, meta e mensagem de boas-vindas.
- Stats Grid: cartões com métricas rápidas (aumento salarial potencial, meses, horas/semana, projetos). Clique nos cartões para acionar uma pequena animação de celebração.
- Tabs: navegação entre as seções — Roadmap, Cursos, Certificações, Ferramentas, ROI Calculator e Dicas para papais.
- Roadmap: timeline com 8 trimestres; cada item tem uma barra de progresso clicável.
- Courses & Certifications: lista de cursos e certificações com links externos.
- Tools: ícones e checklist de ferramentas por trimestre.
- ROI Calculator: inputs para salário atual/meta, custo de investimento e tempo; botão para calcular ROI e mostrar payback e retorno em 5 anos.
- Tips: grade de dicas práticas e seção motivacional final.

### Comportamento JavaScript importante

- Tabs: função `openTab(evt, tabName)` controla exibição das abas.
- ROI: `calculateROI()` calcula aumento mensal, ROI anual, payback e retorno em 5 anos; valida entradas.
- Progress bars: `updateProgress()` anima barras; clicar num `.timeline-item` alterna progresso (0/100) e salva em `localStorage` com chave `progress-<n>`.
- Confetes/celebrações: `celebrate(emoji)` cria elementos flutuantes temporários.
- Easter egg: sequência Konami (via `keydown`) ativa mensagem motivacional e celebração.
- Tooltips: `addTooltips()` adiciona títulos simples aos elementos.
- Countdown: `startCountdown()` cria um contador até 2 anos a partir da data atual.

### Dados esperados / contrato para migração a React (mini-contract)

- Props/estado esperados (exemplos):
  - RoadmapItem: { id, title, description, courses[], progressPercent }
  - CourseCard: { title, description, link, provider }
  - RoiInputs: { currentSalary: number, targetSalary: number, investmentCost: number, timeMonths: number }

- Saídas / efeitos: cálculo de ROI (numbers), persistência de progresso (localStorage), eventos de UI (celebração, navegação entre tabs).

### Sugestão mínima para migrar para React

1. Crie um projeto com Vite ou Create React App.
2. Estruture componentes:
   - `App` (roteador de tabs)
   - `Header`, `StatsGrid`, `Tabs` + `TabContent`
   - `Roadmap` → `TimelineItem`
   - `Courses`, `Certifications`, `Tools`, `Tips`
   - `RoiCalculator` (estado local, validação)
3. Extraia o CSS de `index.html` para um arquivo modular (CSS/SCSS) ou adote CSS-in-JS.
4. Substitua manipulação direta do DOM por estado/props (useState, useEffect). Use localStorage dentro de useEffect para persistência.
5. Adapte animações para CSS ou bibliotecas (framer-motion) se desejar.

Pequeno contrato para `RoiCalculator` em React:
- Inputs: number
- Output: { monthlyIncrease, roiPercentage, paybackMonths, fiveYearReturn }
- Erros: entradas vazias ou target <= current devem retornar mensagem amigável.

## Como ativar GitHub Pages (configuração manual necessária)

**IMPORTANTE**: Após fazer push do código, você precisa configurar manualmente no GitHub:

### Passo 1: Configurar GitHub Pages
1. Vá em: https://github.com/afborda/career-transition-in-2-years/settings/pages
2. Em **"Build and deployment"** → **"Source"**, selecione **"GitHub Actions"** 
   (NÃO selecione "Deploy from a branch")
3. Salve as configurações

### Passo 2: Aguardar o deploy
- A GitHub Action executará automaticamente após push na branch `main`
- Primeiro deploy pode levar até 10 minutos
- Deployments subsequentes são mais rápidos (1-3 minutos)

### URLs disponíveis (após configuração):
- **GitHub Pages padrão**: https://afborda.github.io/career-transition-in-2-years/
- **Domínio personalizado**: https://abnerfonseca.com.br (após configurar DNS)

### Configuração DNS necessária
Para o domínio personalizado funcionar, configure estes registros DNS no seu provedor:

**Registros A** (aponte para os IPs do GitHub Pages):
```
abnerfonseca.com.br  A  185.199.108.153
abnerfonseca.com.br  A  185.199.109.153  
abnerfonseca.com.br  A  185.199.110.153
abnerfonseca.com.br  A  185.199.111.153
```

**Registro CNAME** (opcional, para www):
```
www.abnerfonseca.com.br  CNAME  afborda.github.io
```

#### Como ver localmente (durante desenvolvimento)

1. Abra o arquivo `index.html` no navegador (duplo-clique ou `Open File` no editor).
2. Para servir localmente (opcional), use um servidor estático simples:

```bash
python3 -m http.server 8000
# depois abra http://localhost:8000/
```

### Próximos passos recomendados (se quiser ajuda eu posso):

- Gerar a versão em React (componentes + assets) automaticamente a partir do `index.html`.
- Criar testes unitários pequenos para o `RoiCalculator`.
- Extrair os textos para i18n (pt-BR / en).

## ☁️ Configuração Firebase (Sincronização Multi-Dispositivo)

O site agora suporta sincronização automática entre dispositivos usando Firebase! Siga os passos abaixo:

### 🚀 Passo 1: Criar Projeto Firebase

1. Acesse: https://console.firebase.google.com
2. Clique em **"Criar um projeto"**
3. Nome do projeto: `roadmap-papai-edition` (ou outro nome)
4. **Desative** o Google Analytics (opcional)
5. Clique **"Criar projeto"**

### 🔧 Passo 2: Configurar Authentication

1. No painel do Firebase, vá em **"Authentication"**
2. Clique em **"Começar"**
3. Na aba **"Sign-in method"**, habilite:
   - **Google** (recomendado)
   - **Anônimo** (opcional)

### 📊 Passo 3: Configurar Firestore Database

1. Vá em **"Firestore Database"**
2. Clique **"Criar banco de dados"**
3. Escolha **"Começar no modo de teste"**
4. Selecione uma localização (ex: `southamerica-east1`)

### ⚙️ Passo 4: Obter Configuração

1. Vá em **"Visão geral do projeto"** > ⚙️ **"Configurações do projeto"**
2. Role até **"Seus apps"** e clique **"</>"** (Web)
3. Nome do app: `Roadmap Papai Edition`
4. **COPIE** a configuração que aparece (algo como):

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",
  authDomain: "roadmap-papai-edition.firebaseapp.com",
  projectId: "roadmap-papai-edition",
  storageBucket: "roadmap-papai-edition.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123def456"
};
```

### 🔄 Passo 5: Atualizar o Site

1. Abra o arquivo `index.html`
2. Encontre a seção **"Firebase Configuration"** (linha ~3233)
3. **SUBSTITUA** a configuração demo pela sua:

```javascript
// ANTES (demo):
const firebaseConfig = {
    apiKey: "AIzaSyDemoKey-SubstituirPelaSuaChave",
    // ...
};

// DEPOIS (sua configuração):
const firebaseConfig = {
    apiKey: "AIzaSyC...", // SUA chave aqui
    authDomain: "SEU-PROJETO.firebaseapp.com",
    projectId: "SEU-PROJETO",
    // ... resto da SUA configuração
};
```

### 🎯 Como Usar a Sincronização

1. **Fazer Login**: Clique **"📱 Fazer Login com Google"**
2. **Sincronização Automática**: Dados são salvos automaticamente na nuvem
3. **Outro Dispositivo**: Faça login com a mesma conta Google
4. **Sincronização Manual**: Use **"☁️ Sincronizar Dados"** se necessário

### 🛡️ Configuração de Segurança (Importante!)

Para proteger seus dados, configure as regras do Firestore:

1. Vá em **"Firestore Database"** > **"Regras"**
2. Substitua pelas regras abaixo:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Usuários só podem acessar seus próprios dados
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      
      match /{document=**} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
```

3. Clique **"Publicar"**

### ✅ Recursos da Sincronização

- **🔄 Sync Automático**: Login automático salva/carrega dados
- **📱 Multi-Dispositivo**: Acesse de qualquer lugar
- **💾 Backup Local**: localStorage como fallback
- **🔒 Seguro**: Dados protegidos por autenticação
- **⚡ Rápido**: Sincronização em tempo real

### 🆓 Custos

O plano gratuito do Firebase inclui:
- **50k leituras/dia**
- **20k escritas/dia**  
- **1GB armazenamento**

**Mais que suficiente** para seu roadmap de 24 meses! 🚀

### Status da solicitação

- ✅ Requisito: "gerar um README explicando esse site" — Concluído
- ✅ Requisito: "salvar dados em firebase" — Concluído: Sistema completo de sincronização implementado!

---

🎯 **AGORA SEU ROADMAP ESTÁ PROFISSIONAL**: Dashboard inteligente + Sincronização na nuvem + Interface otimizada para 24 meses de estudos!
