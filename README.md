# Mapa Interativo — GitHub Pages + Google Sheets

Mapa interativo hospedado no GitHub Pages que lê pontos de uma planilha Google e organiza camadas por município.

---

## Estrutura esperada da planilha

| Nome | Município | Tipo | Situação | Contato | Observação | Latitude | Longitude |
|------|-----------|------|----------|---------|------------|----------|-----------|
| Ponto A | São Paulo | ... | ... | ... | ... | -23.5505 | -46.6333 |
| Ponto B | Campinas  | ... | ... | ... | ... | -22.9068 | -47.0626 |

> ⚠️ Os nomes das colunas devem ser exatamente iguais aos configurados no `index.html`.

---

## Passo a passo

### 1. Publicar a planilha como CSV

1. Abra sua planilha no **Google Sheets**
2. Vá em **Arquivo → Compartilhar → Publicar na web**
3. Selecione a aba correta no primeiro menu
4. No segundo menu, selecione **Valores separados por vírgula (.csv)**
5. Clique em **Publicar** e copie a URL gerada

A URL terá o formato:
```
https://docs.google.com/spreadsheets/d/SEU_ID/pub?gid=0&single=true&output=csv
```

---

### 2. Configurar o `index.html`

Abra o arquivo e edite o bloco `CONFIG`:

```javascript
const CONFIG = {
  // Cole aqui a URL CSV copiada no passo anterior
  csvUrl: 'https://docs.google.com/spreadsheets/d/SEU_ID/pub?...',

  col: {
    nome:      'Nome',       // coluna com o nome do ponto
    municipio: 'Município',  // coluna que define as camadas
    lat:       'Latitude',
    lng:       'Longitude',

    campos: [
      { label: 'Tipo',       col: 'Tipo'       },
      { label: 'Situação',   col: 'Situação'   },
      { label: 'Contato',    col: 'Contato'    },
      { label: 'Observação', col: 'Observação' },
    ],
  },

  titulo: 'Mapa de Pontos',   // título exibido no painel lateral
  centro: [-15.77, -47.92],   // centro inicial do mapa [lat, lng]
  zoom:   5,
};
```

> 💡 Ajuste `campos` para refletir os nomes reais das suas colunas.  
> Se tiver 3 campos, basta remover uma entrada do array.

---

### 3. Criar o repositório no GitHub

1. Crie um repositório público (ex: `meu-mapa`)
2. Faça upload do `index.html` na raiz do repositório
3. Vá em **Settings → Pages**
4. Em **Source**, selecione `Deploy from a branch`
5. Selecione `main` / `root` e clique em **Save**

Após alguns minutos, o mapa estará disponível em:
```
https://SEU_USUARIO.github.io/meu-mapa/
```

---

## Atualizar os dados

Basta editar a planilha Google — o mapa carrega os dados em tempo real a cada acesso. Não é necessário atualizar nenhum arquivo no GitHub.

---

## Funcionalidades

| Recurso | Detalhe |
|---------|---------|
| 🗺️ Mapa base | CartoDB Dark Matter (tema escuro) |
| 📍 Marcadores | Cor única por município |
| 🪟 Popup | Exibe nome + 4 campos descritivos estilizados |
| 🧭 Painel lateral | Lista todos os municípios com contagem de pontos |
| 👁️ Toggle de camadas | Clique para mostrar/ocultar cada município |
| 🔘 Recolher painel | Botão lateral para maximizar o mapa |
| 🔍 Auto-zoom | O mapa ajusta o zoom para exibir todos os pontos ao carregar |

---

## Dependências (carregadas via CDN)

- [Leaflet.js 1.9.4](https://leafletjs.com/) — motor do mapa
- [PapaParse 5.4.1](https://www.papaparse.com/) — leitura do CSV
- [Google Fonts](https://fonts.google.com/) — Fraunces + DM Sans
# isoladas
