<!DOCTYPE html>
<html lang='pt-BR'>
    <head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'>
        <style>
            body{font-family:Arial;margin:0;background:#f3f3f3}
            h2{margin:0;background:#1976d2;color:#fff;padding:15px;text-align:center}
            #tot{background:#222;color:#0f0;font-size:38px;text-align:center;padding:15px}
            .g{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;padding:8px}
            button{padding:4px;font-size:14px;border-radius:8px}
            .row{display:flex;justify-content:space-between;align-items:center;background:#fff;margin:6px;padding:8px;border-radius:8px}
            .minus{background:#e53935;color:#fff}
        </style>
    </head>

    <body>
        <h2>Pedido</h2>
        <div id='tot'>R$ 0,00</div>
        <div class='g' id='g'></div><div id='list'></div>
        <button style='width:95%;margin:10px' onclick='clearAll()'>Limpar Pedido</button>
        <script>
            const p=[['Carga Inicial',5],['Macarronada Domingo',30],['Espetinho Carne',18],
                ['Espetinho Frango',13],['Espetinho Kafta',15],['Espetinho Linguiça',15],
                ['Lanche Carne',25],['Lanche Linguiça',20],['Lanche Pernil',25],
                ['Pastel',14],['Cachorro Quente',14],['Mini Pizza',15],
                ['Caldo Verde',18],['Guioza',14],['Pinhão',12],
                ['Batata Frita',12],['Morango com Chocolate',15],['Churros ou Doce de Abóbora',12],
                ['Brigadeiro Gourmet',5],['Caixa Brigadeiro 4 unidades',12],['Curau ou Bolos',12],
                ['Arroz Doce ou Canjica',12],['Café',5],['Cerveja ou Vinho Quente',12],
                ['Suco Natural',12],['Refrigerante',10],['Água',6],
                ['Água c/ Gás',7],['Taça Vinho',18],['Garrafa Vinho',65],
                ['Quentão',9],['Bingo Cartela Simples',8],['Bingo Cartela Especial',15],
                ['Brincaderas',10]];
            let it={},t=0;
            p.forEach(([n,v])=> {
                let b=document.createElement('button');
                b.innerHTML=n+'<br>R$ '+v.toFixed(2).replace('.',',');
                b.onclick=()=>{
                    it[n] =(it[n]||0);
                    if (n ==="Carga Inicial") {
                        if (it[n] === 0) {
                            it[n] = 1;
                            t+=v;
                            draw()
                        }
                    } 
                    else {
                        it[n]=it[n]+1;
                        t+=v;
                        draw()
                    }
                }
                g.appendChild(b);
            });
            function draw()
                {tot.innerText='R$ '+t.toFixed(2).replace('.',',');
                 list.innerHTML='';
                 for(const [n,q] of Object.entries(it))
                     {const v=p.find(x=>x[0]==n)[1];
                      let r=document.createElement('div');
                      r.className='row';
                      r.innerHTML='<div><b>'+q+'x '+n+'</b><br>R$ '+(q*v).toFixed(2).replace('.',',')+'</div>';
                      let m=document.createElement('button');
                      m.className='minus';m.textContent='➖';
                      m.onclick=()=>
                          {it[n]--;
                           t-=v;
                           if(it[n]<=0)delete it[n];
                           draw()
                          };
                      r.appendChild(m);
                      list.appendChild(r);
                     }
                 }
            function clearAll()
                {it={};
                 t=0;
                 draw();
                }
        </script>
    </body>
</html>
