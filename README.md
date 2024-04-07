# ESTOQUE_WEB_APP
Modelo de precificação FG

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Estoque</title>
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
<style>
    body {
        background-color: #f0f7ff; /* Azul claro */
    }
    .container {
        margin-top: 50px;
    }
    .card {
        border: none;
        border-radius: 10px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    .card-header {
        background-color: #007bff; /* Azul */
        color: white;
        border-radius: 10px 10px 0 0;
    }
    .card-body input[type="number"] {
        width: 100%;
        padding: 10px;
        border-radius: 5px;
        border: 1px solid #ced4da; /* Cinza claro */
    }
    .btn {
        background-color: #007bff; /* Azul */
        color: white;
        border: none;
        border-radius: 5px;
        padding: 10px 20px;
    }
    .btn:hover {
        background-color: #0056b3; /* Azul escuro */
    }
</style>
</head>
<body>

<div class="container">
    <div class="row justify-content-center">
        <div class="col-md-6">
            <div class="card">
                <div class="card-header">
                    Adicionar Item ao Estoque
                </div>
                <div class="card-body">
                    <form id="formEstoque">
                        <div class="form-group">
                            <label for="item">Item:</label>
                            <input type="text" id="item" name="item" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="sku">SKU:</label>
                            <input type="text" id="sku" name="sku" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="precoCompra">Preço de Compra:</label>
                            <input type="number" id="precoCompra" name="precoCompra" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="precoVenda">Preço de Venda:</label>
                            <input type="number" id="precoVenda" name="precoVenda" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="outrosCustos">Outros Custos:</label>
                            <input type="number" id="outrosCustos" name="outrosCustos" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="impostos">Impostos (%):</label>
                            <input type="number" id="impostos" name="impostos" step="0.01" min="0" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="valorPromocional">Valor Promocional:</label>
                            <input type="number" id="valorPromocional" name="valorPromocional" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="taxaFixaComissao">Taxa Fixa de Comissão (R$):</label>
                            <input type="number" id="taxaFixaComissao" name="taxaFixaComissao" class="form-control">
                        </div>
                        <button type="button" onclick="adicionarItem()" class="btn btn-block">Adicionar Item</button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <div class="row justify-content-center mt-5">
        <div class="col-md-10">
            <div class="card">
                <div class="card-header">
                    Estoque
                </div>
                <div class="card-body">
                    <table id="tabelaEstoque" class="table">
                        <thead>
                            <tr>
                                <th>Item</th>
                                <th>SKU</th>
                                <th>Preço de Compra</th>
                                <th>Preço de Venda</th>
                                <th>Outros Custos</th>
                                <th>Impostos (%)</th>
                                <th>Valor em Reais (Imposto Fixo 18%)</th>
                                <th>Lucro Líquido</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    function adicionarItem() {
        var item = document.getElementById("item").value;
        var sku = document.getElementById("sku").value;
        var precoCompra = parseFloat(document.getElementById("precoCompra").value);
        var precoVenda = parseFloat(document.getElementById("precoVenda").value);
        var outrosCustos = parseFloat(document.getElementById("outrosCustos").value);
        var impostos = parseFloat(document.getElementById("impostos").value);
        var valorPromocional = parseFloat(document.getElementById("valorPromocional").value);
        var taxaFixaComissao = parseFloat(document.getElementById("taxaFixaComissao").value);
        var impostoFixo = 0.18; // 18% em decimal

        // Cálculos
        var precoTotal = precoCompra + outrosCustos;
        var impostoReais = precoTotal * impostoFixo;
        var precoVendaFinal = precoVenda;
        if (valorPromocional && valorPromocional < precoVenda) {
            precoVendaFinal = valorPromocional;
        }
        var comissao = taxaFixaComissao;
        var lucroLiquido = precoVendaFinal - (precoCompra + outrosCustos + impostoReais + comissao);

        // Adicionando à tabela
        var tabela = document.getElementById("tabelaEstoque").getElementsByTagName('tbody')[0];
        var newRow = tabela.insertRow();
        
        var cell1 = newRow.insertCell(0);
        var cell2 = newRow.insertCell(1);
        var cell3 = newRow.insertCell(2);
        var cell4 = newRow.insert
