# Configuração Mongoose

```javascript
const mongoose = require("mongoose");

module.exports = function(uri) {
  //Definindo o use de Promise Nativa
  mongoose.Promise = global.Promise;

  mongoose.connect("mongodb://" + uri);

  //Ouvindo o evento connected para saber se deu certo a conexão
  mongoose.connection.on("connected", () =>
    console.log("Conectado ao Bancão da Porra")
  );

  //Ouvindo o evento de erro e imprimindo no console caso tenha dado algum problema
  mongoose.connection.on("error", error =>
    console.log("Erro na conexão:", error)
  );

  //Ouvindo o evento de desconexão
  mongoose.connection.on("disconnected", () =>
    console.log("Conexão encerrada do banco de dados")
  );

  //Acesso ao objeto global Process para escutar o evento que for de "Encerramento" da aplicação
  process.on("SIGINT", () =>
    //Quando algo fechar a aplicação, fecha a conexão com o banco também
    mongoose.connection.close(() => {
      console.log("Conexão fechada pelo término da aplicação");
      //Indica que o encerramento foi feito de forma natural (esperado)
      process.exit(0);
    })
  );
};
```
