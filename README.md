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

### Como acessar o site

#### URLs disponíveis (após deploy):
- **Domínio personalizado**: https://abnerfonseca.com.br
- **GitHub Pages padrão**: https://afborda.github.io/career-transition-in-2-years/

#### Configuração DNS necessária
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

### Status da solicitação

- Requisito: "gerar um README explicando esse site" — Concluído: README criado na raiz do repositório (`README.md`).

---

Se quiser, posso: (1) gerar a versão React automaticamente; (2) transformar a UI em componentes e criar um starter com Vite. Diga qual opção prefere.
