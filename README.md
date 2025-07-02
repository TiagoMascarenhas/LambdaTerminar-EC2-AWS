# 💻 Lambda para Terminar Instâncias EC2 na AWS

Este projeto tem como objetivo automatizar o término de instâncias EC2 utilizando uma função AWS Lambda agendada via Amazon EventBridge.

---

## 🧠 Objetivo

Automatizar o encerramento de instâncias EC2 que estejam em estados `running`, `stopped` ou `stopping` nas regiões definidas.

---

## 🛠️ Tecnologias e Serviços Utilizados

- AWS Lambda (Python 3.9)
- AWS IAM (Política personalizada e Role)
- Amazon EC2
- Amazon EventBridge
- CloudWatch (para logs)
- Boto3 (SDK AWS para Python)

---

## 🔧 Estrutura do Projeto

### `Terminator.py`

Script principal que:

1. Itera por regiões específicas (us-east-1, sa-east-1, etc.)
2. Filtra instâncias EC2 com estado `running`, `stopped` ou `stopping`
3. Finaliza essas instâncias usando boto3

---

## 🔐 Permissões

A política criada concede à função Lambda as permissões necessárias para:

- `ec2:DescribeInstances`
- `ec2:TerminateInstances`
- `logs:*` (criação e escrita em CloudWatch Logs)

---

## 🚀 Como Executar

### 1. Crie a política IAM personalizada

Nome: `PoliticaTerminarEC2-TiagoMascarenhas`  
(Ver `policy.json` se disponível)

### 2. Crie a role IAM

Nome: `RoleTerminarEC2-TiagoMascarenhas`  
Associe a política acima à role. Serviço confiável: `Lambda`

### 3. Crie a função Lambda

Nome: `LambdaTerminarEC2-TiagoMascarenhas`  
Tempo de execução: Python 3.9  
Role atribuída: `RoleTerminarEC2-TiagoMascarenhas`  
Upload do código: `Terminator.py`

### 4. Configure o gatilho no EventBridge

Nome: `GatilhoTerminarEC2-TiagoMascarenhas`  
Expressão de agendamento sugerida: `rate(12 hours)` ou `rate(5 minutes)`

---

## 📌 Observações

- O tempo de execução da Lambda foi ajustado para 10 segundos
- Handler configurado como: `Terminator.lambda_handler`
- Logs disponíveis no CloudWatch após execução

---

## 🧽 Cleanup (Limpeza dos recursos)

> Não se esqueça de deletar as funções, roles, políticas e regras EventBridge após os testes para evitar custos desnecessários.

---

## 📸 Prints do Projeto (opcional)

Você pode visualizar abaixo algumas imagens do projeto funcionando no console AWS:

- Criação de política IAM
- Role configurada
- Função Lambda com código
- EventBridge configurado
