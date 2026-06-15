<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <title>Grafo Interativo</title>
    
    <!-- Importação do Vis.js para visualização do grafo -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/vis-network/9.1.2/dist/vis-network.min.css" integrity="sha512-WgxfT5LWjfszlPHXRmBWHkV2eceiWTOBvrKCNbdgDYTHrT2AeLCGbF4sZlZw3UMN3WtL0tGUoIAKsu8mllg/XA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vis-network/9.1.2/dist/vis-network.min.js" integrity="sha512-LnvoEWDFrqGHlHmDD2101OrLcbsfkrzoSpvtSQtxK3RMnRV0eOkhhBN2dXHKRrUU8p2DGRTk35n4O8nWSVe1mQ==" crossorigin="anonymous"></script>
    
    <style>
        /* Garantindo que o grafo ocupe 100% da tela */
        html, body {
            margin: 0;
            padding: 0;
            width: 100vw;
            height: 100vh;
            overflow: hidden;
        }

        #mynetwork {
            width: 100vw;
            height: 100vh;
            background-color: #ffffff;
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>

    <div id="mynetwork"></div>

    <script>
        // Ajustar o tamanho do grafo para ocupar 100% do iframe
        window.onload = function() {
            var container = document.getElementById('mynetwork');
            container.style.width = window.innerWidth + "px";
            container.style.height = window.innerHeight + "px";
        };

        // Definição de nós e arestas
        var nodes = new vis.DataSet([
            { id: "Jair Bolsonaro", label: "Jair Bolsonaro", shape: "dot", size: 50, color: "#33FFF3" },
            { id: "Forças Armadas", label: "Forças Armadas", shape: "dot", size: 50, color: "#FFBD33" },
            { id: "Militares", label: "Militares", shape: "dot", size: 50, color: "#3357FF" },
            { id: "Exército", label: "Exército", shape: "dot", size: 50, color: "#33FF57" },
            { id: "Trump", label: "Trump", shape: "dot", size: 50, color: "#FF3333" },
            { id: "Lula", label: "Lula", shape: "dot", size: 50, color: "#FF5733" },
            { id: "Alexandre De Moraes", label: "Alexandre De Moraes", shape: "dot", size: 50, color: "#9B33FF" },
            { id: "Patriotas", label: "Patriotas", shape: "dot", size: 50, color: "#FF5733" },
            { id: "Povo", label: "Povo", shape: "dot", size: 50, color: "#FFBD33" },
            { id: "Caminhoneiros", label: "Caminhoneiros", shape: "dot", size: 50, color: "#FF3333" }
        ]);

        var edges = new vis.DataSet([
            { from: "Jair Bolsonaro", to: "Forças Armadas", label: "OPPOSES", arrows: "to", color: "#FFBD33", width: 3 },
            { from: "Jair Bolsonaro", to: "Militares", label: "WORKED_AT", arrows: "to", color: "#FF5733", width: 1 },
            { from: "Forças Armadas", to: "Lula", label: "OPPOSES", arrows: "to", color: "#FFBD33", width: 3 },
            { from: "Forças Armadas", to: "Patriotas", label: "SUPPORTS", arrows: "to", color: "#9B33FF", width: 4 },
            { from: "Militares", to: "Patriotas", label: "SUPPORTS", arrows: "to", color: "#9B33FF", width: 7 },
            { from: "Exército", to: "Lula", label: "SUPPORTS", arrows: "to", color: "#9B33FF", width: 1 },
            { from: "Povo", to: "Jair Bolsonaro", label: "SUPPORTS", arrows: "to", color: "#9B33FF", width: 6 }
        ]);

        // Configuração do grafo
        var container = document.getElementById("mynetwork");
        var data = { nodes: nodes, edges: edges };
        var options = {
            interaction: {
                dragNodes: true,
                hideEdgesOnDrag: false,
                hideNodesOnDrag: false
            },
            physics: {
                enabled: true,
                forceAtlas2Based: {
                    avoidOverlap: 0,
                    centralGravity: 0.01,
                    damping: 0.5,
                    gravitationalConstant: -50,
                    springConstant: 0.08,
                    springLength: 300
                },
                solver: "forceAtlas2Based",
                stabilization: {
                    enabled: true,
                    fit: true,
                    iterations: 1000,
                    onlyDynamicEdges: false,
                    updateInterval: 50
                }
            }
        };

        var network = new vis.Network(container, data, options);
    </script>

</body>
</html>
