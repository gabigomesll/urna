# urna
URNA: GABRIELA PASSARELA GOMES - 201 . 

<?php 
    session_start();
    //$_SESSION['mensagem']="";
    $r = "";
    $x = @$_GET['digito'];
    $r = $x;
    @$_SESSION['tela'] = $_SESSION['tela'] . $r;
   // echo $_SESSION['tela'];
   if((@$_GET['voto'] == 13) || (@$_GET['voto'] == 45) || (@$_GET['voto'] == 24)){
    if(@$_GET['confirmar'] == 'confirmar'){
        //confirmar
        //gravar o voto;
        $votos = @$_GET['voto'];
        $arquivo = "votos.txt";
        $conteudo = "$votos, ";
        $abertura = fopen($arquivo,"a");
        
        $gravacao = fwrite($abertura, $conteudo);
        fseek($abertura, 0);
        $leitura = fread($abertura, filesize($arquivo));
        fclose($abertura);
        unset($_SESSION['tela']);  
        echo "VOTO CONFIRMADO";
    }
    }else if(((@$_GET['voto'] == '') || (@$_GET['branco'] == 'branco') ) && (@$_GET['confirmar'] == 'confirmar')){
        //branco
        $votos = @$_GET['voto'];
        $arquivo = "brancos.txt";
        $conteudo = "$votos, ";
        $abertura = fopen($arquivo,"a");
        $gravacao = fwrite($abertura, $conteudo);
        fseek($abertura, 0);
        $leitura = fread($abertura, filesize($arquivo));
        fclose($abertura);
        unset($_SESSION['tela']);
         echo "VOTO BRANCO";
        
    }else if(@$_GET['corrigir'] == 'corrigir'){
        //limpar
        unset($_SESSION['tela']);
    }else if((@$_GET['voto'] != 13) || (@$_GET['voto'] != 45) || (@$_GET['voto'] != 24)){
        if(@$_GET['confirmar'] == 'confirmar'){
        //limpar
        // gravar o voto nulo
         $votos = @$_GET['voto'];
        $arquivo = "nulos.txt";
        $conteudo = "$votos, ";
        $abertura = fopen($arquivo,"a");
        
        $gravacao = fwrite($abertura, $conteudo);
        fseek($abertura, 0);
        $leitura = fread($abertura, filesize($arquivo));
        fclose($abertura);
        unset($_SESSION['tela']);
        echo "VOTO NULO";
        }   
    }
?>
<html>
    <head>
        <meta charset="UTF-8">
    </head>
    <body >
        <h2>URNA ELETRONICA</h2>
        <?php echo @$_SESSION['mensagem']; ?>
        <form action="" method="get" border="1px">
            <div id="numero">
                <label>PRESIDENTE</label><br/>
                <input type="text" value="<?php echo @$_SESSION['tela']; ?>" name="voto" readonly="">
            </div>
            <div id="teclado">
                <input type="submit" name="digito" value="1"/>
		<input type="submit" name="digito" value="2"/>
		<input type="submit" name="digito" value="3"/><br />
		<input type="submit" name="digito" value="4"/>
		<input type="submit" name="digito" value="5"/>
		<input type="submit" name="digito" value="6"/><br />
		<input type="submit" name="digito" value="7"/>
		<input type="submit" name="digito" value="8"/>
		<input type="submit" name="digito" value="9"/><br />
		<input type="submit" name="digito" value="0"/><br />
		<button type="submit" name="branco" value="branco">Branco</button>
                <button type="reset" name="corrigir" value="corrigir">Corrigir</button>
                <button type="submit" name="confirmar" value="confirmar">Confirmar</button>
            </div>
        </form>
        
    </body>
</html>
