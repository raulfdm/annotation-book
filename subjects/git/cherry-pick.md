# Cherry pick

O comando `git cherry-pick` no git é muito útil para os momentos onde precisamos pegar apenas um commit especifico de um determinado `branch`, sem precisar trazer TODAS as alterações.

Então, imagine o seguinte cenário: Alguém abriu um `pull request` com várias features. Porém, você percebe que um determinado commit impacta em uma feature que você está trabalhando. Ao invés de pegar TODAS as alterações e trazer pro seu branch em formato de rebase/merge, você quer apenas pegar aquele commit especifíco e testar. É nesses casos que o `cherry-pick` vai te ajudar.

## How to

1. Vá para o branch que você deseja pegar a alteração (`git checkout featureA`);
1. Digite log e pegue o hash do commit que deseja extrair;
1. Volte para seu branch (`git checkout myCustomFeature`);
1. Digite o comando `git cherry-pick {numero-do-hash}`;

Feito isso, todas as alterações daquele commit serão aplicados no branch que você está trabalhando.
