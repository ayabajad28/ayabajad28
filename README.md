<!DOCTYPE html>
<html lang="fr">
 <head>
<meta charset="UTF-8">
 <title>Exercice Transaction</title>
 </head>
 <body>

 <h2>Formulaire de Transaction</h2>

 <div>
 <label for="produit">Produit :</label>
 <select id="produit">
 </select>
 <input type="text" id="nouveauProduit" placeholder="Ajouter un nouveau produit">
 <button id="ajouterProduit">Ajouter Produit</button>
 </div>

 <div>
<label for="prix">Prix :</label>
<input type="number" id="prix">
 </div>

 <div>
 <label for="quantite">Quantité :</label>
 <input type="number" id="quantite">
 </div>

 <button id="ajouterTransaction">Ajouter Transaction</button>

 <h2>Transactions</h2>
 <table id="tableauTransactions">
<thead>
 <tr>
 <th>Produit</th>
 <th>Prix</th>
 <th>Quantité</th>
 <th>Total</th>
 </tr>
 </thead>
 <tbody>
</tbody>
 </table>

 <div>
 <p>Total des prix: <span id="totalPrix">0</span></p>
 <p>Nombre de transactions: <span id="nombreTransactions">0</span></p>
 </div>

 <script>
    document.addEventListener("DOMContentLoaded", function() {
    const selectProduit = document.getElementById("produit");
    const inputNouveauProduit = document.getElementById("nouveauProduit");
    const inputPrix = document.getElementById("prix");
    const inputQuantite = document.getElementById("quantite");
    const btnAjouterProduit = document.getElementById("ajouterProduit");
    const btnAjouterTransaction = document.getElementById("ajouterTransaction");
    const tableauTransactions = document.getElementById("tableauTransactions");
    const spanTotalPrix = document.getElementById("totalPrix");
    const spanNombreTransactions = document.getElementById("nombreTransactions");
    let totalPrix = 0;
    let nombreTransactions = 0;

    btnAjouterProduit.addEventListener("click", function() {
        const nouveauProduit = inputNouveauProduit.value.trim();
        if (nouveauProduit !== "") {
            const option = document.createElement("option");
            option.textContent = nouveauProduit;
            selectProduit.appendChild(option);
            inputNouveauProduit.value = "";
        }
    });
    btnAjouterTransaction.addEventListener("click", function() {
        const produit = selectProduit.value.trim();
        const prix = parseFloat(inputPrix.value);
        const quantite = parseInt(inputQuantite.value);

        if (produit !== "" && !isNaN(prix) && !isNaN(quantite) && prix > 0 && quantite > 0) {
            const total = prix * quantite;
            totalPrix += total;
            nombreTransactions++;

            const newRow = tableauTransactions.insertRow(-1);
            const cellProduit = newRow.insertCell(0);
            const cellPrix = newRow.insertCell(1);
            const cellQuantite = newRow.insertCell(2);
            const cellTotal = newRow.insertCell(3);

            cellProduit.textContent = produit;
            cellPrix.textContent = prix.toFixed(2);
            cellQuantite.textContent = quantite;
            cellTotal.textContent = total.toFixed(2);

            spanTotalPrix.textContent = totalPrix.toFixed(2);
            spanNombreTransactions.textContent = nombreTransactions;
            inputPrix.value = "";
            inputQuantite.value = "";
        } else {
            alert("Veuillez remplir correctement tous les champs.");
        }
    });
});

 </script>

 </body>
 </html>
