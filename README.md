# 📄 Projeto: Automação de Cotação de Moedas com UiPath

## 🎯 Objetivo

Desenvolver uma automação com UiPath que:

1. Acesse o site do Banco Central do Brasil.
2. Extraia a cotação atual do **Dólar (USD)** e do **Euro (EUR)** em relação ao Real (BRL).
3. Gere um **PDF** com as informações extraídas e a **data/hora** da consulta.
4. Simule o **envio desse PDF por e-mail** (comentado, por segurança e simplicidade).

---

## 🔧 Tecnologias utilizadas

- **UiPath Studio**
- **Activities:** 
  - Use Application/Browser
  - Get Text
  - Assign
  - Write Text File
  - Word Application Scope
  - Export to PDF
  - Send SMTP Mail Message (comentado)
- Site utilizado: [https://www.bcb.gov.br](https://www.bcb.gov.br)

---

## 🧠 Lógica do Fluxo (`Main.xaml`)

1. **Início do fluxo**
   - O processo começa com uma **sequência principal**.

2. **Abrir navegador**
   - Usa a atividade **Use Application/Browser** para abrir o site:  
     `https://www.bcb.gov.br/estabilidadefinanceira/historicocotacoes`.

3. **Extração das cotações**
   - Localiza na página as cotações do Dólar e do Euro utilizando **Get Text**.
   - Armazena em variáveis `cotacaoDolar` e `cotacaoEuro`.

4. **Obter data e hora atual**
   - Usa `Now.ToString("dd/MM/yyyy HH:mm:ss")` e armazena em `dataConsulta`.

5. **Gerar conteúdo do relatório**
   - Usa **Assign** para montar o conteúdo do relatório:
     ```vb
     conteudoPDF = $"Cotação de moedas - Consulta em {dataConsulta}{vbCrLf}" &
                   $"Dólar (USD): R$ {cotacaoDolar}{vbCrLf}" &
                   $"Euro  (EUR): R$ {cotacaoEuro}"
     ```

6. **Salvar conteúdo como PDF**
   - Usa **Write Text File** para salvar o conteúdo como `.txt`.
   - Em seguida, usa **Word Application Scope + Export to PDF** ou **Invoke Code** para gerar o arquivo `Cotacoes.pdf`.

7. **Simular envio de e-mail**
   - Adiciona a atividade `Send SMTP Mail Message`, mas **comenta o envio**.
   - Os campos como SMTP, senha e destinatário são deixados configuráveis.

8. **Encerrar processo**
   - O processo fecha o navegador automaticamente.

---

## 📤 Simulação do Envio de E-mail

- A automação já inclui a atividade de envio de e-mail (`Send SMTP Mail Message`).
- Para segurança, está **comentada**.
- Basta configurar:
  - SMTP (ex: smtp.gmail.com)
  - Porta (ex: 587)
  - Usuário/senha (usar credenciais seguras)
  - Anexar o arquivo `Cotacoes.pdf`

---

## 📂 Estrutura de Arquivos


---

## ✅ Como Executar

1. Abra o projeto no **UiPath Studio**.
2. Execute o `Main.xaml`.
3. Verifique o PDF gerado na pasta do projeto.
4. Se desejar, configure o envio de e-mail (SMTP) e **descomente** a parte do código de envio.
