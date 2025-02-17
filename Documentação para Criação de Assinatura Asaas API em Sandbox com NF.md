# Criar Nova Assinatura

## Método

* `POST`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions`

## Descrição

Criar uma nova assinatura. Ao criar a assinatura, a primeira mensalidade será gerada vencendo na data enviada no parâmetro `nextDueDate`.

## Período de Gratuidade

Sim, é possível criar assinaturas com período de gratuidade. Se você trabalha com um período de trial (7 dias grátis, por exemplo), poderá seguir da mesma forma e informar no campo `nextDueDate` a data da primeira cobrança.

## Body Params

* `customer` (string, obrigatório): Identificador único do cliente no Asaas
* `billingType` (string, obrigatório): Forma de pagamento
	+ `UNDEFINED`
* `value` (number, obrigatório): Valor da assinatura
* `nextDueDate` (date, obrigatório): Vencimento da primeira cobrança
* `discount` (object, opcional): Informações de desconto
	+ `discount` (object)
* `interest` (object, opcional): Informações de juros para pagamento após o vencimento
	+ `interest` (object)
* `fine` (object, opcional): Informações de multa para pagamento após o vencimento
	+ `fine` (object)
* `cycle` (string, obrigatório): Periodicidade da cobrança
	+ `WEEKLY`
* `description` (string, opcional): Descrição da assinatura (máx. 500 caracteres)
* `endDate` (date, opcional): Data limite para vencimento das cobranças
* `maxPayments` (int32, opcional): Número máximo de cobranças a serem geradas para esta assinatura
* `externalReference` (string, opcional): Identificador da assinatura no seu sistema
* `split` (array of objects, opcional): Informações de split
	+ `ADD` (object)
* `callback` (object, opcional): Informações de redirecionamento automático após pagamento do link de pagamento
	+ `callback` (object)

## Respostas

* `200 OK`
* `401 Unauthorized`








# Listar Assinaturas

## Método

* `GET`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions`

## Descrição

Listar todas as assinaturas para os filtros informados. Diferente da recuperação de uma assinatura específica, este método retorna uma lista paginada.

## Exemplos de uso

* Listar assinaturas de um cliente específico: `GET https://api.asaas.com/v3/subscriptions?customer={customer_id}`
* Filtrar por forma de pagamento: `GET https://api.asaas.com/v3/subscriptions?billingType=CREDIT_CARD`

## Query Params

* `offset` (integer): Elemento inicial da lista
* `limit` (integer): Número de elementos da lista (max: 100)
* `customer` (string): Filtrar pelo Identificador único do cliente
* `customerGroupName` (string): Filtrar pelo nome do grupo de cliente
* `billingType` (string): Filtrar por forma de pagamento
	+ `UNDEFINED`
* `status` (string): Filtrar pelo status
	+ `ACTIVE`
* `deletedOnly` (string): Envie `true` para retornar somente as assinaturas removidas
* `includeDeleted` (string): Envie `true` para recuperar também as assinaturas removidas
* `externalReference` (string): Filtrar pelo Identificador do seu sistema
* `order` (string): Ordem crescente ou decrescente
* `sort` (string): Por qual campo será ordenado

## Respostas

* `200 OK`
* `401 Unauthorized`
* `403 Forbidden`: Ocorre quando o body da requisição está preenchido, chamadas de método GET precisam ter um body vazio







# Criar Assinatura com Cartão de Crédito

## Método

* `POST`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/`

## Descrição

Criar uma assinatura com cartão de crédito. Os dados do cartão e do portador podem ser enviados na requisição de criação da assinatura para que o pagamento já seja processado.

## Atenção

* É obrigatório o uso de SSL (HTTPS) ao capturar os dados do cartão do cliente.
* Recomenda-se configurar um timeout mínimo de 60 segundos para evitar timeouts e duplicidades na captura.

## Tokenização de Cartão de Crédito

* Para utilizar a tokenização de cartão de crédito, siga as mesmas instruções do Criar cobrança com cartão de crédito.

## Body Params

* `customer` (string, obrigatório): Identificador único do cliente no Asaas
* `billingType` (string, obrigatório): Forma de pagamento
	+ `UNDEFINED`
* `value` (number, obrigatório): Valor da assinatura
* `nextDueDate` (date, obrigatório): Vencimento da primeira cobrança
* `discount` (object, opcional): Informações de desconto
	+ `discount` (object)
* `interest` (object, opcional): Informações de juros para pagamento após o vencimento
	+ `interest` (object)
* `fine` (object, opcional): Informações de multa para pagamento após o vencimento
	+ `fine` (object)
* `cycle` (string, obrigatório): Periodicidade da cobrança
	+ `WEEKLY`
* `description` (string, opcional): Descrição da assinatura (máx. 500 caracteres)
* `endDate` (date, opcional): Data limite para vencimento das cobranças
* `maxPayments` (int32, opcional): Número máximo de cobranças a serem geradas para esta assinatura
* `externalReference` (string, opcional): Identificador da assinatura no seu sistema
* `split` (array of objects, opcional): Informações de split
	+ `ADD` (object)
* `callback` (object, opcional): Informações de redirecionamento automático após pagamento do link de pagamento
	+ `callback` (object)
* `creditCard` (object, opcional): Informações do cartão de crédito
	+ `creditCard` (object)
* `creditCardHolderInfo` (object, opcional): Informações do titular do cartão de crédito
	+ `creditCardHolderInfo` (object)
* `creditCardToken` (string, opcional): Token do cartão de crédito para uso da funcionalidade de tokenização de cartão de crédito
* `remoteIp` (string, obrigatório): IP de onde o cliente está fazendo a compra

## Respostas

* `200 OK`
* `401 Unauthorized`






# Recuperar uma Única Assinatura

## Método

* `GET`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}`

## Descrição

Recuperar uma assinatura específica. Para isso, é necessário ter o ID da assinatura, que é retornado pelo Asaas no momento da criação.

## Observação

* Para recuperar as cobranças de uma assinatura, utilize o método Listar cobranças de uma assinatura.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Respostas

* `200 OK`
* `401 Unauthorized`
* `403 Forbidden`: Ocorre quando o body da requisição está preenchido, chamadas de método GET precisam ter um body vazio.
* `404 Not found`




# Atualizar Assinatura Existente

## Método

* `PUT`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}`

## Descrição

Atualizar uma assinatura existente. Ao atualizar uma assinatura, o parâmetro `nextDueDate` serve para indicar o vencimento da próxima mensalidade a ser gerada, ou seja, não atualiza o vencimento da mensalidade já gerada.

## Observações

* Ao atualizar o valor da assinatura ou forma de pagamento, somente serão afetadas mensalidades futuras.
* Para atualizar as mensalidades já existentes com a nova forma de pagamento e/ou novo valor, é necessário passar o parâmetro `updatePendingPayments: true`.
* É possível suspender a assinatura informando o status como `INACTIVE`. Isso fará com que novas cobranças deixem de ser geradas até que seja setado como `ACTIVE` novamente.
* Ao retomar uma assinatura, é obrigatório informar o `nextDueDate` da próxima assinatura gerada.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Body Params

* `billingType` (string, opcional): Forma de pagamento
	+ `BOLETO`
* `status` (string, opcional): Status da assinatura
	+ `ACTIVE`
* `nextDueDate` (date, opcional): Vencimento da primeira cobrança
* `discount` (object, opcional): Informações de desconto
	+ `discount` (object)
* `interest` (object, opcional): Informações de juros para pagamento após o vencimento
	+ `interest` (object)
* `fine` (object, opcional): Informações de multa para pagamento após o vencimento
	+ `fine` (object)
* `cycle` (string, opcional): Periodicidade da cobrança
	+ `MONTHLY`
* `description` (string, opcional): Descrição da assinatura (máx. 500 caracteres)
* `endDate` (date, opcional): Data limite para vencimento das cobranças
* `updatePendingPayments` (boolean, opcional): `true` para atualizar as propriedades possíveis de cobranças pendentes já existentes
* `externalReference` (string, opcional): Identificador da assinatura no seu sistema
* `split` (array of objects, opcional): Informações de split
	+ `ADD` (object)
* `callback` (object, opcional): Informações de redirecionamento automático após pagamento do link de pagamento
	+ `callback` (object)

## Respostas

* `200 OK`
* `401 Unauthorized`
* `404 Not found`





# Remover Assinatura

## Método

* `DELETE`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}`

## Descrição

Remover uma assinatura. Ao remover uma assinatura, as mensalidades aguardando pagamento ou vencidas também são removidas.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Respostas

* `200 OK`
* `401 Unauthorized`
* `404 Not found`




# Listar Cobranças de uma Assinatura

## Método

* `GET`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/payments`

## Descrição

Listar as cobranças de uma assinatura específica.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Query Params

* `status` (string, opcional): Filtrar por status das cobranças
	+ `PENDING`

## Respostas

* `200 OK`
* `401 Unauthorized`
* `403 Forbidden`: Ocorre quando o body da requisição está preenchido, chamadas de método GET precisam ter um body vazio.
* `404 Not found`






# Gerar Carnê de Assinatura

## Método

* `GET`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/paymentBook`

## Descrição

Gerar um carnê de assinatura para uma assinatura específica.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Query Params

* `month` (integer, obrigatório): Mês final para geração do carnê
* `year` (integer, obrigatório): Ano final para geração do carnê
* `sort` (string, opcional): Filtrar pelo nome da coluna
* `order` (string, opcional): Ordenação da coluna

## Respostas

* `200 OK`
* `401 Unauthorized`
* `403 Forbidden`: Ocorre quando o body da requisição está preenchido, chamadas de método GET precisam ter um body vazio.
* `404 Not found`







# Criar Configuração para Emissão de Notas Fiscais

## Método

* `POST`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoiceSettings`

## Descrição

Criar uma configuração para emissão de Notas Fiscais para uma assinatura específica.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Body Params

* `municipalServiceId` (string, opcional): Identificador único do serviço municipal
* `municipalServiceCode` (string, opcional): Código de serviço municipal
* `municipalServiceName` (string, opcional): Nome do serviço municipal
* `updatePayment` (boolean, opcional): Atualizar o valor da cobrança com os impostos da nota já descontados
* `deductions` (number, opcional): Deduções. As deduções não alteram o valor total da nota fiscal, mas alteram a base de cálculo do ISS
* `effectiveDatePeriod` (string, opcional): Quando a nota fiscal será emitida
	+ `ON_PAYMENT_CONFIRMATION`
* `receivedOnly` (boolean, opcional): Emitir apenas para cobranças pagas
* `daysBeforeDueDate` (int32, opcional): Quantidade de dias antes do vencimento da cobrança
* `observations` (string, opcional): Observações adicionais da nota fiscal
* `taxes` (object, opcional): Impostos da nota fiscal
	+ `taxes` (object)

## Respostas

* `200 OK`
* `401 Unauthorized`
* `404 Not found`






# Recuperar Configuração para Emissão de Notas Fiscais

## Método

* `GET`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoiceSettings`

## Descrição

Recuperar a configuração para emissão de notas fiscais de uma assinatura específica.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Respostas

* `200 OK`
* `401 Unauthorized`
* `403 Forbidden`: Ocorre quando o body da requisição está preenchido, chamadas de método GET precisam ter um body vazio.
* `404 Not found`







# Remover Configuração para Emissão de Notas Fiscais

## Método

* `DELETE`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoiceSettings`

## Descrição

Remover a configuração para emissão de notas fiscais de uma assinatura específica. Ao remover a configuração, todas as notas fiscais agendadas para as cobranças desta assinatura serão canceladas e sua geração automática será interrompida.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Respostas

* `200 OK`
* `401 Unauthorized`
* `404 Not found`







# Atualizar Configuração para Emissão de Notas Fiscais

## Método

* `PUT`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoiceSettings`

## Descrição

Atualizar a configuração para emissão de notas fiscais de uma assinatura específica. A nova configuração apenas será aplicada nas notas fiscais das próximas cobranças da assinatura, ou as que ainda não possuem uma nota fiscal criada.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Body Params

* `deductions` (number, opcional): Deduções. As deduções não alteram o valor total da nota fiscal, mas alteram a base de cálculo do ISS
* `effectiveDatePeriod` (string, opcional): Quando a nota fiscal será emitida
	+ `ON_PAYMENT_CONFIRMATION`
* `receivedOnly` (boolean, opcional): Emitir apenas para cobranças pagas
* `daysBeforeDueDate` (int32, opcional): Quantidade de dias antes do vencimento da cobrança
* `observations` (string, opcional): Observações adicionais da nota fiscal
* `taxes` (object, opcional): Impostos da nota fiscal
	+ `taxes` (object)

## Respostas

* `200 OK`
* `401 Unauthorized`
* `404 Not found`





# Listar Notas Fiscais das Cobranças de uma Assinatura

## Método

* `GET`

## URL

* `https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoices`

## Descrição

Listar todas as notas fiscais geradas a partir de cobranças de uma assinatura específica. O método retorna uma lista paginada e é possível filtrar o status e período de emissão das notas fiscais.

## Path Params

* `id` (string, obrigatório): Identificador único da assinatura no Asaas

## Query Params

* `offset` (integer, opcional): Elemento inicial da lista
* `limit` (integer, opcional): Número de elementos da lista (max: 100)
* `effectiveDate[ge]` (string, opcional): Filtrar a partir de uma data de emissão
* `effectiveDate[le]` (string, opcional): Filtrar até uma data de emissão
* `externalReference` (string, opcional): Identificador da nota fiscal no seu sistema
* `status` (string, opcional): Filtrar por status da nota fiscal
	+ `SCHEDULED`
* `customer` (string, opcional): Filtrar pelo identificador único do cliente

## Respostas

* `200 OK`
* `401 Unauthorized`
* `403 Forbidden`: Ocorre quando o body da requisição está preenchido, chamadas de método GET precisam ter um body vazio.
* `404 Not found`





Exemplo de Requisição cURL
curl --request GET \
  https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoices \
  --header 'accept: application/json'






Exemplo de Requisição em PHP:

<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoices",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => [
    "accept: application/json"
  ],
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}

?>






Exemplo de Requisição Guzzle:
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api-sandbox.asaas.com/v3/subscriptions/{id}/invoices', [
  'headers' => [
    'accept' => 'application/json',
  ],
]);

echo $response->getBody();


OBS.: Substitua {id} pelo identificador único da assinatura no Asaas.