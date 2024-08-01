<<<<<<< HEAD
=======
# Documentação de Validação de CPF e E-mail

## 1. Validação de CPF

### 1.1 Descrição

O código de validação de CPF verifica se o número do CPF inserido pelo usuário é válido. Ele remove caracteres não numéricos e realiza a validação de acordo com as regras matemáticas padrão do CPF.

### 1.2 Estrutura do Código

#### 1.2.1 Manipulação de Eventos

```javascript
document.getElementById("cpfForm").addEventListener("submit", function (event) {
  event.preventDefault();

  const cpf = document.getElementById("cpf").value;
  const msg = document.getElementById("message");
  if (validateCPF(cpf)) {
    msg.textContent = "O CPF é Válido";
    msg.style.color = 'green';
  } else {
    msg.textContent = "O CPF é inválido";
    msg.style.color = 'red';
  }
});
```

- **Descrição:** Adiciona um ouvinte de evento ao formulário que é acionado ao ser submetido. O evento padrão de submissão é prevenido e a função `validateCPF` é chamada para verificar a validade do CPF.

#### 1.2.2 Função de Validação do CPF

```javascript
function validateCPF(cpf){
   cpf = cpf.replace(/[^\d]+/g, ''); // Remove caracteres não numéricos
 
   // Verifica se o CPF tem 11 dígitos e se todos são iguais
    if(cpf.length !== 11 || /^(\d)\1{10}$/.test(cpf)){
        return false;
    }
    
    let soma = 0;
    let resto;

    // Valida o primeiro dígito verificador
    for(let i = 1; i < 9; i++){
      soma += parseInt(cpf.substring(i-1, i)) * (11 - i);
    }
    resto = (soma * 10) % 11;
    if((resto === 10) || (resto === 11)){
      resto = 0;
    }
    if(resto !== parseInt(cpf.substring(9,10))){
      return false;
    }
    
    soma = 0;
    
    // Valida o segundo dígito verificador
    for(let i = 1; i <= 10; i++){
      soma += parseInt(cpf.substring(i - 1, i)) * (12 - i);
    }
    resto = (soma * 10) % 11;
    if((resto === 10) || (resto === 11)){
      resto = 0;
    }
    if(resto !== parseInt(cpf.substring(10,11))){
      return false;
    }
    
    return true;
}
```

- **Descrição:** A função `validateCPF` realiza as seguintes etapas:
  1. Remove caracteres não numéricos do CPF.
  2. Verifica se o CPF tem exatamente 11 dígitos e se não é composto por todos os mesmos dígitos.
  3. Calcula e valida o primeiro e o segundo dígito verificador do CPF conforme as regras matemáticas.

### 1.3 Como Usar

1. Inclua um formulário HTML com um campo para CPF e uma área para mostrar mensagens.
2. Certifique-se de que o formulário tem o id `cpfForm`, o campo de entrada de CPF tem o id `cpf`, e a área para mensagens tem o id `message`.
3. Adicione o código JavaScript ao seu HTML para habilitar a validação.

## 2. Validação de E-mail

### 2.1 Descrição

O código de validação de e-mail verifica se o e-mail inserido pelo usuário é válido, garantindo que ele contenha "@" e ".".

### 2.2 Estrutura do Código

#### 2.2.1 Função de Validação de E-mail

```javascript
function ChecarEmail() {
    if (document.forms[0].email.value == "" ||
        document.forms[0].email.value.indexOf("@") == -1 ||
        document.forms[0].email.value.indexOf(".") == -1) {
        alert("Por favor informe um e-mail válido");
        return false;
    } else {
        alert("E-mail informado com sucesso!");
    }
}
```

- **Descrição:** A função `ChecarEmail` realiza a validação do e-mail verificando:
  1. Se o campo de e-mail não está vazio.
  2. Se o e-mail contém pelo menos um "@" e um ".".
  3. Exibe uma mensagem de alerta com base na validade do e-mail e retorna `false` se o e-mail não for válido.

### 2.3 Como Usar

1. Inclua um formulário HTML com um campo para e-mail.
2. Adicione o código JavaScript ao seu HTML para realizar a validação quando necessário.

## 3. Considerações Finais

- Certifique-se de incluir ambos os scripts JavaScript em seu HTML e referenciar corretamente os IDs e nomes dos campos de formulário.
- Adapte as mensagens e a lógica conforme necessário para atender às suas necessidades específicas.

>>>>>>> 3fc8a43f78bc04d3431fa49a0b29e2a3af32c664
