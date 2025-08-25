# Lista de Bancos do Brasil – JSON (ISPB)

Este repositório contém a lista de bancos brasileiros em formato JSON. Os dados são derivados do Banco Central do Brasil (Participantes do STR).

Cada registro no arquivo `banks.json` possui a seguinte estrutura:

```json
{
  "ISPB": 92894922,
  "Nome_Reduzido": "BANCO ORIGINAL",
  "Número_Código": 212,
  "Participa_da_Compe": "Sim",
  "Acesso_Principal": "RSFN",
  "Nome_Extenso": "Banco Original S.A.",
  "Início_da_Operação": "22/04/2002"
}
```

---

## Acesso ao arquivo

### Raw (GitHub)

```
https://raw.githubusercontent.com/marcosantdm/bancos-br-ispb/main/banks.json
```

### CDN (jsDelivr)

```
https://cdn.jsdelivr.net/gh/marcosantdm/bancos-br-ispb@latest/banks.json
```

---

## Exemplos de Consumo

### cURL

```bash
curl -s https://raw.githubusercontent.com/marcosantdm/bancos-br-ispb/main/banks.json | jq '.[0]'
```

### JavaScript (fetch)

```js
fetch('https://cdn.jsdelivr.net/gh/marcosantdm/bancos-br-ispb@latest/banks.json')
  .then(r => r.json())
  .then(data => {
    const bancoOriginal = data.find(b => b["Número_Código"] === 212);
    console.log(bancoOriginal);
  });
```

### Node.js (Axios)

```js
import axios from 'axios';

const url = 'https://raw.githubusercontent.com/marcosantdm/bancos-br-ispb/main/banks.json';
const { data } = await axios.get(url, { timeout: 10000 });
console.log(`Total de registros: ${data.length}`);
```

### PHP (Laravel HTTP Client)

```php
$response = Http::timeout(10)->get('https://raw.githubusercontent.com/marcosantdm/bancos-br-ispb/main/banks.json');
$banks = $response->json();

$original = collect($banks)->firstWhere('Número_Código', 212);
```

### Python (requests)

```python
import requests
url = "https://cdn.jsdelivr.net/gh/marcosantdm/bancos-br-ispb@latest/banks.json"
resp = requests.get(url, timeout=10)
resp.raise_for_status()
banks = resp.json()
print(banks[0])
```

---

## Consultas no cliente

### Buscar por ISPB

```js
data.find(b => b.ISPB === 92894922)
```

### Buscar por código COMPE

```js
data.find(b => b["Número_Código"] === 1)
```

### Buscar por parte do nome

```js
data.filter(b => b.Nome_Extenso.toUpperCase().includes('BRASIL'))
```

---

## Fonte Oficial

Banco Central do Brasil – Participantes do STR: [https://www.bcb.gov.br/estabilidadefinanceira/participantesstr](https://www.bcb.gov.br/estabilidadefinanceira/participantesstr)

---

## Licença

MIT — livre para uso em projetos pessoais e comerciais.
