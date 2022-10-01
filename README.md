# jogo-da-velha
Curso ibm


<!DOCTYPE html>
<html lang="pt-BR">
    <head>
        <title>Jogo da Velha</title>
        <link rel="stylesheet" type="text/css" href="css/style.css" />
        
        
        <script type="text/javascript" src="js/jquery-3.2.1.min.js"></script>
        
        
        <script type="text/javascript">
            var interval = null;
            $(document).ready(function(){
                
                //Validação de preenchimento
                $("#btn_comecar").click(function(){
                    var jog1 = $("input[name=jogador1]").val();
                    var jog2 = $("input[name=jogador2]").val();
                    
                    if( jog1.trim().length > 0 && jog2.trim().length > 0){
                        //Começar o jogo
                        $(".msg").text("");
                        ComecarJogo();
                        
                    }else{
                        $(".msg").text("Nome(s) não preenchido");
                    }
                });
            });
            
            function ComecarJogo(){
                var contadorClicks = 0;
                
                interval = setInterval(TempoDecorrido, 500);
                
                $("table td").click(function(){
                    contadorClicks++;
                    
                    if( contadorClicks <= 9 ){
                        if( contadorClicks % 2 == 0 ){
                            //Par
                            $(this).text("O");
                        }else{
                            //Impa
                            $(this).text("X");
                        }
                        
                        
                        if( VerificarGanhador() == true ){
                            contadorClicks = 9;
                        }
                        
                        if( contadorClicks == 9){
                            $(".msg").append("<br />Jogo encerrado");
                            clearInterval(interval);
                        }
                    }
                });
            }
            
            function VerificarGanhador(){
                var vencedor = [
                    //Linhas
                    [0, 1, 2],
                    [3, 4, 5],
                    [6, 7, 8],
                    //Colunas
                    [0, 3, 6],
                    [1, 4, 7],
                    [2, 5, 8],
                    //Diagonais
                    [0, 4, 8],
                    [6, 4, 2]
                ];

                var X = new Array(9);
                var O = new Array(9);
                $("table td").each(function(key, value){
                    if( $(this).text() == "X" ){
                        X[key] = key;
                    }
                    if( $(this).text() == "O" ){
                        O[key] = key;
                    }
                });
                return DefinirGanhador(X, O, vencedor);
            }
            function DefinirGanhador(X, O, vencedor){
                //Percorre as linhas.
                for(var i = 0; i < vencedor.length; i++){
                    contadorX = 0;
                    contadorO = 0;

                    //Percorre as colunas de uma linha
                    for(var y = 0; y < vencedor[i].length; y++){
                        if( X[vencedor[i][y]] == vencedor[i][y]){
                            contadorX++;
                        }

                        if( O[vencedor[i][y]] == vencedor[i][y]){
                            contadorO++;
                        }
                        vencedor[i][y]
                    }
                    
                    var jog1 = $("input[name=jogador1]").val();
                    var jog2 = $("input[name=jogador2]").val();
                    if(contadorX == 3){
                        $(".msg").text("X - " + jog1 + " Ganhou");
                        return true;
                    }
                    if( contadorO == 3){
                        $(".msg").text("O - " + jog2 + " Ganhou");
                        return true;
                    }
                } 
            }
            var inicioJogo = null;
            function TempoDecorrido(){
                if(inicioJogo == null){
                    inicioJogo = new Date();
                }
                var dataAtual = new Date();
                
                var segIni = inicioJogo.getSeconds();
                var segAtual = dataAtual.getSeconds();
                
                var minIni = inicioJogo.getMinutes();
                var minAtual = dataAtual.getMinutes();
                
                var horaIni = inicioJogo.getHours();
                var horaAtual = dataAtual.getHours();
                
                var timeIni = inicioJogo.getTime();
                var timeAtual = dataAtual.getTime();
                
                var timeDec = timeAtual - timeIni;
                
                var novaData = new Date(timeDec);
                
                
                $("#tempo").text("Inicío do Jogo: " + horaIni + ":" + minIni + ":" + segIni + 
                                 " - Hora atual: " + horaAtual +":"+ minAtual + ":" + segAtual + 
                                 " - Tempo Decorrido: " + novaData.getMinutes() + ":" + novaData.getSeconds()
                                );
            }
        </script>
        
    </head>
    <body>
        <div class="configurador">
            <div class="msg">
                
            </div>
            <span>X</span><input type="text" name="jogador1" placeholder="Nome Jogador 1" />
            
            x
            <input type="text" name="jogador2" placeholder="Nome Jogador 2" /><span>O</span>
            
            <br />
            <br />
            <button id="btn_comecar">Começar Jogo</button>
            <br />
            
        </div>
        <table>
            <tr>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </table>
        <div id="tempo">00:00</div>
        
        
        
        
        <!--
        <h3>Salário</h3>
        <table>
            <tr>
                <td rowspan="2">José</td>
                <td>R$ 3.000,00</td>
                <td rowspan="2">R$ 5.200,00</td>
            </tr>
            <tr>
                <td>R$ 1.200,00</td>
            </tr>
            <tr>
                <td>Maria</td>
                <td colspan="2">R$ 2.500,00</td>
            </tr>
        </table>
        -->
    </body>
</html>
Footer
© 2022 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
