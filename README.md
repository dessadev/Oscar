# 🎬 E o Oscar vai para...? 
Banco de dados sobre o Oscar, contendo informações sobre indicados e vencedores de diferentes categorias ao longo dos anos.

E o Oscar vai para...? 

01. Quantas vezes Natalie Portman foi indicada ao Oscar?
Q: db["oscar"].countDocuments({ "nome_do_indicado": "Natalie Portman" });
R: 03 indicações.

--------------------------------------

02. Quantos Oscars Natalie Portman ganhou?
Q: db["oscar"].countDocuments({ "nome_do_indicado": "Natalie Portman", "vencedor": "true" });
R: 01 Oscar.

--------------------------------------

03. Amy Adams já ganhou algum Oscar?
Q: db["oscar"].countDocuments({ "nome_do_indicado": "Amy Adams", "vencedor": "true" });
R: Amy Adams não ganhou nenhum Oscar.

--------------------------------------

04. A série de filmes Toy Story ganhou um Oscar em quais anos?
Q: db["oscar"].find({"nome_do_filme": /Toy Story/,"vencedor": "true"}, {"ano_cerimonia": 1, "nome_do_filme": 1, "_id": 0});
R: Foram 3 Oscar (anos: 2011 e 2020)

--------------------------------------

05. A partir de que ano que a categoria "Actress" deixa de existir? 
Q: db["oscar"].find({ "categoria": "ACTRESS" }).sort({ "ano_cerimonia": -1 }).limit(1);
R: A partir de 1976.

--------------------------------------

06. O primeiro Oscar para melhor Atriz foi para quem? Em que ano?
Q: db["oscar"].find({ "categoria": "ACTRESS", "vencedor": "true" }).sort({ "ano_cerimonia": 1 }).limit(1);
R: Janet Gaynor em 1929.

--------------------------------------

07. Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.
Q: db["oscar"].updateMany({ "vencedor": "true" },{ $set: { "vencedor": 1 } });
db["oscar"].updateMany({ "vencedor": "false" },{ $set: { "vencedor": 0 } });
R: Feito.

--------------------------------------

08. Em qual edição do Oscar "Crash" concorreu ao Oscar?
Q: db["oscar"].find({ "nome_do_filme": "Crash" },{ "ano_cerimonia": 1, "categoria": 1 });
R: Ano de 2006.

--------------------------------------

09. Bom... dê um Oscar para um filme que merece muito, mas não ganhou.
Q: db["oscar"].updateOne({ _id: ObjectId('6716c529912aee072f398be0') },{ $set: { "vencedor": 1 } });
R: Central do Brasil (Central Station).

----------------------------------------------------------------------------

10.  O filme Central do Brasil aparece no Oscar?
Q: db.oscar.find({ "nome_do_filme": "Central Station" });
R: 1999.

----------------------------------------------------------------------------

11. Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 
Q: db["oscar"].insertMany([
    {
        "id_registro": null,
        "ano_filmagem": 1999,
        "ano_cerimonia": 2000,
        "cerimonia": 72,
        "categoria": "Melhor Filme",
        "nome_do_indicado": "Clube da Luta",
        "nome_do_filme": "Fight Club",
        "vencedor": false
    },
    {
        "id_registro": null,
        "ano_filmagem": 1993,
        "ano_cerimonia": 1994,
        "cerimonia": 66,
        "categoria": "Melhor Filme de Animação",
        "nome_do_indicado": "O Estranho Mundo de Jack",
        "nome_do_filme": "The Nightmare Before Christmas",
        "vencedor": false
    },
    {
        "id_registro": null,
        "ano_filmagem": 1997,
        "ano_cerimonia": 1999,
        "cerimonia": 71,
        "categoria": "Melhor Filme",
        "nome_do_indicado": "A Vida é Bela",
        "nome_do_filme": "Life is Beautiful",
        "vencedor": false
    }
]);
R:  Adicionei "Fight Club", "The Nightmare Before Christmas" e "Life is Beautiful".

----------------------------------------------------------------------------

12. Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?
Q: db.oscar.find({"ano_cerimonia": 2002, "categoria": { $regex: /actress|picture|directing/i }, "vencedor": 1 },
    { "categoria": 1, "nome_do_filme": 1, "nome_do_indicado": 1 });
R: Melhor Filme: "A Beautiful Mind" - Melhor Atriz: Halle Berry por "Monster's Ball" - Melhor Diretor: Ron Howard por "A Beautiful Mind"




