# Consulta_SQL_SSMS

-- Nesse projeto realizei algumas Consultas para criar indicadores interessantes a serem analisados. <br>
-- Fiz uso de clausula como JOiN, GROUP BY, ORDER BY e WHERE que proporcionam analises mais assertivas. <br>
-- Como também fiz uso de Subqueries que me ajudam a realizar as consultas em varias etapas dando maior poder de manipulação dos dados. <br>

**Indicativo de Metas dos Colaboradores Empresa X** <br>

Aparti do Esquema de relacionamento abaixo <br>
<img src="https://github.com/matheus-oliveir4/Consulta_SQL_SSMS/blob/main/Esquema_Realacional.PNG" alt=" esquemas" width = 800px> <br>

**Consulta**


    use EMPRESA_DB
    
    Select
    	C2.NomeCompleto,
    	C2.Cargo,
    	Format(C2.Valor,'C', 'pt-BR') Valor,
    	C2.Quantidade,
    	Format(C2.[Valor Total], 'C', 'pt-BR') [Valor total vendido],
    	CASE WHEN C2.[Valor Total] >= 20000000
    		THEN 'Atingiu'
    	ELSE
    		 'Não Atingiu'
    	END AS [Status]
    From
    
    (SELECT
    	F.NomeCompleto,
    	F.Cargo,
    	C1.Valor,
    	C1.Quantidade,
    	C1.[Valor Total]
     
    FROM

    (Select
		p.FuncionarioId,
		Sum(D.Preco) [Valor],
		Sum(D.Quantidade) Quantidade,
		SUM(D.Preco) * sum(D.Quantidade) [Valor Total] 
	From 
		TB_PEDIDO as P 
	join
		TB_DETALHE_PEDIDO D ON P.NumeroPedido = D.NumeroPedido
	GROUP BY 
		P.FuncionarioId) AS C1
	join 
		TB_FUNCIONARIO F On C1.FuncionarioId = F.FuncionarioId) As C2 



Resultados <br>

<img src="https://github.com/matheus-oliveir4/Consulta_SQL_SSMS/blob/main/Resultado01.PNG" alt="Resultado" width = 800px> <br>

