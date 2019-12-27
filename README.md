# normas_firmware
Algumas normas de firmware para desenvolvimento em C

# Nomas de desenvolvimento de firmware em C

### Índice
- [Introdução](#idIntro)
    - [Propósito](#idIntroProposito)
    - [Princípios Orientadores](#IdIntroPrincipios)
    - [Exceções](#IdIntroExcecoes)
- [1 - Regras Gerais](#IdRegra1)
    - [1.1 - Compiladores](#IdRegra1.1)
    - [1.2 - Larguras de linha](#IdRegra1.2)
    - [1.3 - Chaves](#IdRegra1.3)
    - [1.4 - Parênteses](#IdRegra1.4)
    - [1.5 - Abreviações comuns](#IdRegra1.5)
    - [1.6 - Conversão de tipo (type casting)](#IdRegra1.6)
    - [1.7 - Palavras chaves a evitar](#IdRegra1.7)
    - [1.8 - Palavras chaves que devem ser frequentes](#IdRegra1.8)
                
    
***
<a name="idIntro"></a>
## Introdução

>“Um bom estilo de programação começa com a organização efetiva do código. Usando uma organização clara e consistente dos componentes de seu programa, você torna-os mais eficiente, legível e de fácil manutenção.”

> [Steve Oualline](http://www.oualline.com/), [C Elements of Style](http://www.oualline.com/style/index.html)

<a name="idIntroProposito"></a>
#### PROPÓSITO

Este documento define a forma normalizada que todos os programadores deverão criar software embarcado (também conhecido como firmware). Todo programador deve estar intimamente familiarizado com esta Norma, entender e aceitar essas exigências. Todos os consultores e prestadores de serviços também deverão aderir a esta Norma.

A razão para esta Norma é de garantir que o desenvolvimento de firmware da **Omnilink** atenda aos níveis mínimos de legibilidade e de facilidade de manutenção.

O código fonte tem **DUAS** funções igualmente importantes que são: ele **DEVE FUNCIONAR**, e ele deve claramente **COMUNICAR COMO ELE FUNCIONA** para um futuro programador ou futuras versões do mesmo. Assim como os padrões de gramática e ortografia da língua portuguesa fazem uma narração legível, uma convenção padronizada de código facilita a leitura do próprio firmware.

Um código que tem um bom estilo é definido como aquele que é:

- Organizado
- Fácil de ler
- Fácil de entender
- Fácil de dar manutenção
- Eficiente

Outra razão para a adoção desta Norma é a de reduzir o número de erros presentes em novos firmwares e em códigos adicionados ou modificados posteriormente por mantenedores.

É claro que uma Norma de codificação por si só não elimina todos os erros de um sistema embarcado complexo. Ela é apenas uma parte de um processo de desenvolvimento. As outras partes do processo tem que enfatizar o papel fundamental da formação do desenvolvedor, arquitetura de software e de sistema, processo eficaz e leve, e a cultura de uma equipe ou da organização em manter um software livre de erros.

***
<a name="IdIntroPrincipios"></a>
#### PRINCÍPIOS ORIENTADORES

Esta norma de codificação foi desenvolvida de acordo com os seguintes princípios orientadores, que serviram para concentrar a atenção dos autores e eliminar conflitos sobre itens que são vistos, algumas vezes por programadores, como preferências estilísticas pessoais:

1. Programadores individuais não são os donos do software que eles escrevem.^[1](#IdFootnote01)^ Todo o desenvolvimento de software é um trabalho por contrato para um empregador ou um cliente e, portanto, o produto final deve ser construído de maneira profissional.

2. É mais barato e mais fácil prevenir que um erro entre no código do que é para encontrá-lo e eliminá-lo depois que já entrou. Uma estratégia chave nessa luta é escrever código na qual o compilador, linker ou ferramenta de análise estática possam detectar erros automaticamente, ou seja, antes que o código seja permitido executar.

3. Para melhor ou pior (bem, na maior parte pior), a “normalização” ISO de linguagem de programação C permite uma quantidade significativa de variabilidade das decisões tomadas pelos fornecedores de compiladores. Estes comportamentos muitas vezes assim chamados de “definidos pela aplicação”, “não especificados” ou “indefinidos”, juntamente com opções específicas de cada compilador, significa que programas compilados de códigos-fonte C idênticos podem se comportar de forma diferente em tempo de execução. Tais áreas obscuras na normalização da linguagem reduzem a portabilidade de programas em C que não são cuidadosamente preparados.

4. A confiabilidade^[2](#IdFootnote02)^, legibilidade, eficiência e às vezes portabilidade do código fonte são mais importantes que a conveniência do programador. 

5. Existem muitas fontes de defeitos em programas de software. A equipe original de programadores criará alguns defeitos. Os programadores que posteriormente mantêm, estendem, portam e/ou reutilizam o código fonte resultante podem criar defeitos adicionais - inclusive como resultado de imcompreensões do código original.
    1. O número e a gravidade de erros introduzidos pelo(s) programador(es) original(is) podem ser reduzidos através de conformidade disciplinada com algumas práticas de codificação, tais como a colocação de constantes no lado esquerdo de um teste de equivalência ( == ).
    2. O número e a gravidade dos erros introduzidos pelos programadores que fazem a manutenção também podem ser reduzidos pelo programador original. Por exemplo, o uso adequado de tipos inteiros de largura fixa portáveis (por exemplo, int32_t) garante que nenhum futuro reuso do código vai encontrar um overflow inesperado.
    3. O número e a gravidade dos erros introduzidos por programadores que fazem a manutenção também podem ser reduzidos através do uso disciplinado de práticas consistentes de comentários e estilização, para que todos na organização possam entender mais facilmente o significado e uso adequado de variáveis, funções e módulos.
 
6. Para ser eficaz, os padrões de codificação devem ser aplicáveis. Assim, quando duas ou mais regras alternativas impediriam igualmente defeitos, a regra mais facilmente aplicada é a melhor escolha.

Na ausência de uma regra necessária neste documento ou de um conflito dentro do padrão de codificação que sua equipe se compromete a seguir, o espírito dos princípios acima deve ser aplicado para orientar a decisão.

***
<a name="IdIntroExcecoes"></a>
#### EXCEÇÕES

Parte de cada revisão de código é para garantir aos módulos e funções revisadas satisfazer os requisitos da norma. Códigos que não se encontram dentro do padrão serão rejeitados. Nós reconhecemos que nenhum padrão pode cobrir todas as eventualidades. Pode haver ocasiões onde fará sentido abrir uma exceção para um ou mais requerimentos incorporados neste documento. Toda exceção deve conter os seguintes requerimentos:

- **Razão Clara** – Antes de criar uma exceção a Norma, o(s) programador(es) irá(ão) definir claramente e compreender as razões envolvidas, e comunicará(ão) estas razões ao supervisor responsável. As razões devem envolver benefícios claros ao projeto e/ou a Omnilink; motivações de estilo, ou preferências do programador ou peculiaridades não são razões adequadas para tornar uma exceção.
- **Aprovação** – O superior responsável aprovará todas as exceções efetuadas.
- **Documentação** – O módulo ou função afetado deverá ter a exceção claramente documentada nos comentários, então durante a revisão de código ou manutenção posterior a equipe técnica entenderá os motivos e a natureza da exceção.

***
<a name="IdRegra1"></a>
## 1 - Regras Gerais
<a name="IdRegra1.1"></a>
### 1.1 - Compiladores
<a name="IdRegra1.1.a"></a> 
#### Regra 1.1.a
Todos os programas devem ser escritos de acordo com a versão C99 da norma^[3](#IdFootnote03)^ de linguagem de programação ISO C.

<a name="IdRegra1.1.b"></a> 
#### Regra 1.1.b
Sempre que um compilador **C++** é usado, opções apropriadas de compilação devem ser definidas para restringir a linguagem à versão selecionada da ISO C.

<a name="IdRegra1.1.c"></a>
#### Regra 1.1.c
O uso de palavras chaves para extensões proprietárias de linguagens de compiladores, **#pragmas** e "assembly inline" devem ser mantidos ao mínimo necessário para realizar o trabalho, e localizado em um pequeno número de módulos de driver de dispositivo que fazem interface diretamente com o hardware.

<a name="IdRegra1.1.d"></a>
#### Regra 1.1.d
A diretiva de pré-processador **#define** não deve ser usada para alterar ou renomear qualquer palavra-chave ou outro aspecto da linguagem de programação.

##### Exemplo:

    #define begin	{	// Não faça algo como isso...
    #define end	}	// ... nem isso.
    ...
    for (int row = 0; row < MAX_ROWS; row++) 
    begin
        ...
    end	                // Let C be C, not some language you once loved.
    
> **Razão**: 
Para definir claramente as regras no restante deste padrão, é importante que primeiro concordemos com a especificação da linguagem de programação de linha de base.

> **Aplicação**: 
Essas regras devem ser aplicadas via configuração do compilador e revisões de código.

<a name="IdRegra1.2"></a>
### 1.2 - Larguras de linha
<a name="IdRegra1.2.a"></a>
#### Regra 1.2.a
A largura de todas as linhas de um programa deve ser limitada a um máximo de 80 caracteres

> **Razão**: 
Revisões de código e outros tipos de inspeções tendem a ser conduzidos utilizando páginas impressas, e estas devem estar livres de algumas distrações como quebras de linhas bem como caracteres faltando. Essa regra também facilita a visualização do código na tela.

<a name="IdRegra1.3"></a>
### 1.3 - Chaves
<a name="IdRegra1.3.a"></a>
#### Regra 1.3.a
Chaves (**{** e **}**) devem sempre cercar blocos de códigos (também conhecidas como instruções compostas) depois de instruções de

    if
    else
    switch
    while
    do
    for

Mesmo blocos com uma única instrução ou vazios devem sempre ser cercadas por chaves.

<a name="IdRegra1.3.b"></a>
#### Regra 1.3.b
Cada chave esquerda (**{**) deve aparecer sozinha na linha abaixo do início do bloco que ela abre. A chave direita (**}**) correspondente deve aparecer sozinha na mesma posição com o número apropriado de linhas após o bloco.

##### Exemplos:
	// instrução com bloco vazio
	while (0 == TMR0IF)
	{
	 	// Do Nothing
	}
	 
	// instrução com bloco vazio
	if (0 == x)
	{
		PORTA = 1;
	}
	 
	// Observe as posições das chaves:
	while (0 == TMR0IF)
	{
		if (0 == x)
		{
		 	PORTA = 1;
		}
	}
> **Razão**:
Há um risco considerável associado à presença de blocos com uma única instrução ou vazios que não são cercados por chaves. Construções de código como estes são muitas vezes associados a erros quando o código próximo é alterado ou comentado. Este risco é totalmente eliminado pelo uso consistente de chaves. O posicionamento da chave esquerda na linha seguinte permite uma fácil verificação visual da chave direita correspondente.

>**Aplicação**:
A presença de uma chave esquerda após cada **if**, **else**, **switch**, **while**, **do** e **for** deve ser verificado por uma ferramenta de análise no momento da criação. A mesma ferramenta ou outra (como um formatador de código) deve ser usada para reforçar o alinhamento de chaves.

<a name="IdRegra1.4"></a>
### 1.4 - Parênteses
<a name="IdRegra1.4.a"></a>
#### Regra 1.4.a
Não confie nas regras de precedência de operadores da linguagem C, já que elas podem não ser óbvias para aqueles que darão manutenção no código. Para aumentar a clareza, use parênteses (e/ou quebre expressões longas em múltiplas linhas de código) para garantir a ordem de execução apropriada dentro de uma sequência de operação.

<a name="IdRegra1.4.b"></a>
#### Regra 1.4.b
A menos que seja um identificador simples ou uma constante, cada operando das operações lógicas '&&' e '||' devem ser cercados por parênteses.

##### Exemplos:
	if ((a < b) && (b < c))
	{
	    result = (3 * a) + b;
	}
	 
	return result;
	
>**Razão**:
A linguagem C tem muitos operadores. As regras de precedência que determinam quais operadores são executados primeiro são complicados - com mais de uma dúzia de níveis de prioridade - e nem sempre são óbvios para todos os programadores. Em caso de dúvida, é melhor ser explícito sobre o que você espera que o compilador faça com seus cálculos.

>**Aplicação**:
Essas regras devem ser aplicadas durante as revisões de código.

<a name="IdRegra1.5"></a>
### 1.5 - Abreviações comuns

<a name="IdRegra1.5.a"></a>
#### Regra 1.5.a
Abreviaturas e siglas devem ser evitadas a menos que seus significados são ampla e consistentemente reconhecidos pela indústria, como por exemplo USB, PWM, LED, DSP, ADC, LCD, etc.

<a name="IdRegra1.5.b"></a>
#### Regra 1.5.b
Uma tabela de abreviações e siglas adicionais específicas do projeto deve ser mantida em um documento dentro do controle de versão.

>**Razão**:
Os programadores usam facilmente abreviações e siglas enigmáticas em seu código (e em seus currículos!). Só porque você sabe o que ZYZGXL significa hoje não significa que os programadores que precisam ler / manter / portar seu código poderão, posteriormente, entender seus nomes enigmáticos que o referenciam.

>**Aplicação**:
Essas regras devem ser aplicadas durante as revisões de código.

<a name="IdRegra1.6"></a>
### 1.6 - Conversão de tipo (type casting)

<a name="IdRegra1.6.a"></a>
#### Regra 1.6.a
Cada conversão deve apresentar um comentário associado descrevendo como o código garante um comportamento adequado em toda intervalo de possíveis valores do lado direito.

##### Exemplo:
	int32_t abs(int arg)
	{
	    return ((arg < 0) ? -arg : arg);
	}
	...
	uint16_t sample = adc_read(ADC_CHANNEL_1);
	result = abs((int) sample);    /* WARNING: 32-bit int assumed. */
	 


>**Razão**:
Conversões são perigosas. No exemplo acima, a variável "sample" de 16 bits não sinalizada pode conter valores positivos maiores que um número inteiro de 16 bits sinalizado. Neste caso, o valor absoluto estará incorreto também. Portanto, existe um possível estouro se int for de apenas 16 bits, permitido pelo padrão ISO C. A conversão acima parece ter sido usada para silenciar um aviso importante sobre a possível perda de precisão.

>**Aplicação**: 
essas regras devem ser aplicadas durante as revisões de código.

<a name="IdRegra1.7"></a>
### 1.7 - Palavras chaves a evitar

<a name="IdRegra1.7.a"></a>
#### Regra 1.7.a

A palavra chave **auto** não deverá ser usada.

<a name="IdRegra1.7.b"></a>
#### Regra 1.7.b
A palavra chave **register** não deverá ser usada.

<a name="IdRegra1.7.c"></a>
#### Regra 1.7.c
É preferível evitar todo o uso da palavra-chave **goto**. Se o **goto** for usado, ele somente saltará para um **label** declarado posteriormente no mesmo bloco ou em um "enclosing block".

<a name="IdRegra1.7.d"></a>
#### Regra 1.7.d
É preferível evitar todo o uso da palavra-chave **continue**.

>**Razão**:
A palavra chave auto é um recurso da linguagem desnecessário. Alguns outros recursos da linguagem C tem um propósito, mas cria mais dor de cabeça do que valor. Por exemplo, a palavra chave register presume que o programador é mais inteligente do que o compilador. Não há motivo convincente para usar qualquer uma dessas palavras-chave na prática moderna de programação.
As palavras-chave **goto** e **continue** ainda tem propósito na linguagem, mas o uso delas geralmente resultam em código espaguete (spaghetti code). Em particular, o uso do **goto** para fazer saltos ortogonais aos fluxos de controle comuns do paradigma de programação estruturada é problemático. O uso ocasional de goto para lidar com uma circunstância excepcional é aceitável se simplificar e esclarecer o código.

>**Aplicação**: A presença de palavras-chave proibidas no código-fonte novo ou modificado deve ser detectada e relatada por meio de uma ferramenta automatizada a cada compilação. Na medida em que o uso de **goto** ou **continue** é permitido, os revisores de código devem investigar estruturas alternativas de código para melhorar a capacidade de manutenção e legibilidade do código.
 
<a name="IdRegra1.8"></a>
### 1.8 - Palavras chaves que devem ser frequentes

<a name="IdRegra1.8.a"></a>
#### Regra 1.8.a
A palavra chave **static** deve ser usada para declarar todas as funções e variáveis que não precisam ser visíveis fora do módulo na qual eles foram declarados.

<a name="IdRegra1.8.b"></a>
#### Regra 1.8.b
A palavra chave **const** deve ser usada toda vez que for apropriado. Exemplos incluem:
- Para declarar variáveis que não deveriam ser alteradas depois da inicialização.
- Para definir parâmetros de funções chamados por referência que não deveriam ser modificadas (e.g., `char const param`)
- Para definir campos em **structs** e **unions** que não deveriam ser modificadas (e.g, em uma struct que cobre o mapa de memória dos registradores de periféricos de I/O)
- Para definir uma alternativa fortemente tipável ao **#define** para constantes numéricas.

<a name="IdRegra1.8.c"></a>
#### Regra 1.8.c
A palavra chave **volatile** deve ser usada toda vez que for apropriado. Exemplos incluem:
- Para declarar uma variável global acessível (pelo uso atual ou por escopo) por qualquer rotina de serviço de interrupção.
- Para declarar uma variável global acessível (pelo uso atual ou por escopo) por duas ou mais tarefas
- Para declarar um ponteiro para um conjunto de mapa de memória do registrador de periférico de I/O (e.g., timer_t volatile * const p_timer) (??? Tradução desta frase deverá ser revisada ???) To declare a pointer to a memory-mapped I/O peripheral register set (e.g., timer_t volatile * const p_timer)
- Para declarar um contador de loop de delay.

##### Exemplo:

	typedef struct
	{
	    uint16_t	      count;
	    uint16_t	      max_count;
	    uint16_t const    _unused;    /* read-only register */
	    uint16_t	      control;
	} timer_reg_t;

	timer_reg_t volatile * const p_timer = (timer_reg_t *) HW_TIMER_ADDR;

>**Razão**:
A palavra chave **static** tem vários significados. No nível de módulo, variáveis globais e funções declaradas como estáticas são protegidas do uso externo. Use opressivamente static desta maneira que desta forma o acoplamento entre módulos irá diminuir.
As palavras chave **const** e **volatile** são ainda mais importantes. A vantagem de usar **const**, tanto quanto possível é o reforço do lado do compilador na proteção contra escrita indesejada nos dados que devem ser somente leitura.
O uso adequado de **volatile** elimina toda uma classe de bugs difíceis de detectar através da prevenção as otimizações do compilador que eliminaria leituras ou escritas necessárias para variáveis ​​ou registros.^[4](#IdFootnote04)^

>**Aplicação**: 
essas regras devem ser aplicadas durante as revisões de código.

***
<a name="IdRegra2"></a>
## 2 - Módulos
<a name="IdRegra2.1"></a>
### 2.1 - Convenções de nomes:
<a name="IdRegra2.1.a"></a>
#### Regra - 2.1.a:
Todos os nomes dos módulos serão constituídos inteiramente de letras minúsculas, números e underlines (ex.: normas_de_desenvolvimento). Nenhum espaço deverá aparecer dentro do nome do arquivo.

<a name="IdRegra2.1.b"></a>
#### ~~Regra - 2.1.b:~~
~~Todos os nomes dos módulos serão únicos nos seus primeiros oito caracteres, utilizando .h e .c como sufixo para os arquivos de cabeçalho (header) e código fonte, respectivamente.~~

<a name="IdRegra2.1.c"></a>
#### Regra - 2.1.c:
Nenhum nome de módulo poderá compartilhar o mesmo nome dos arquivos da biblioteca padrão do C, como por exemplo “stdio” ou “math”

<a name="IdRegra2.1.d"></a>
#### Regra - 2.1.d:
Qualquer módulo contendo uma função main() deverá ter a palavra “main” no nome do arquivo.
>**Razão**:
Projetos grandes podem requerer várias dúzias de módulos; procurar em uma lista de arquivos dentro de um diretório aquele módulo que contém a função main() pode ser frustrante e confuso.

>**Razão**:
Aumentar a portabilidade entre Windows e Linux. Além disso, nomes misturando maiúsculas e minúsculas estão sujeitos a erros devido à possibilidade de arquivos nomeados de forma semelhante mas capitalizados de forma diferente se tornarem confusos.

>**Razão**: Os ambientes de desenvolvimento de várias plataformas (por exemplo, Unix e Windows) são a norma e não a exceção. Nomes de casos mistos podem causar problemas nos sistemas operacionais e também são propensos a erros devido à possibilidade de arquivos com nomes semelhantes, mas com letras maiúsculas diferentes, serem confundidos por programadores humanos.
A inclusão de "main" em um nome de arquivo é uma ajuda aos mantenedores de código que se mostraram úteis em projetos com várias configurações de software.

> **Aplicação**: Uma ferramenta automatizada deve confirmar que todos os nomes de arquivo que fazem parte de uma compilação são consistentes com essas regras.

### Arquivos de cabeçalho (.h):
#### Regra - 2.5:
Deverá haver sempre precisamente um arquivo de cabeçalho (.h) para cada arquivo fonte (.c) e eles deverão ter sempre o mesmo nome.

Ex:
adc.c
e

adc.h
Razão:
Esta regra é uma convenção, pois o compilador não vê diferença entre um arquivo .c, .h ou qualquer outra extensão. A convenção é que nos arquivos de cabeçalho fiquem as declarações e nos arquivos fonte fiquem as definições.

Regra - 2.6:
Cada arquivo de cabeçalho (.h) deverá conter um protetor de pré-processamento contra inclusões múltiplas, como mostrado no exemplo abaixo:

    #ifndef ADC_H
 
    #define ADC_H
 
    #endif /* ADC_H */
Razão:
Esta técnica, conhecida por #include guard, evita que um cabeçalho (header) seja incluído múltiplas vezes.

Regra - 2.7:
O arquivo de cabeçalho (.h) deverá identificar somente as funções, constantes e tipos de dados (via protótipos ou macros, #define e typedefs dos tipos struct/union/enum, respectivamente) nas quais são estritamente necessário outros módulos conhecerem.

Regra - 2.7.a:
É recomendado que não hajam variáveis declaradas (via extern) em um arquivo de cabeçalho.

Regra - 2.7.b:
Nenhum armazenamento para qualquer variável deve ser declarada em um arquivo de cabeçalho.

Razão:
A intenção é reduzir o acoplamento inter-módulos, mantenha escondidos dentro do módulo fonte (.c) o máximo possível de funções, constantes, tipos de dados e variáveis.

Arquivos fontes (.c):
Regra - 2.8:
Cada arquivo fonte deve incluir apenas os comportamentos adequados para controlar uma “entidade”. Exemplos de entidades incluem tipos de dados encapsulados, objetos ativos, drivers de periféricos (e.g., UARTA), e protocolos ou camadas de comunicação (e.g., ARP).

Regra - 2.9:
Cada arquivo fonte deve ser composto de algumas ou todas das seguintes seções, na ordem listada: bloco de comentários; declarações de include, tipos de dados, constantes e definições de macros, declarações de dados privados (static), protótipos de funções privadas (static), corpo das funções públicas e então o corpo das funções privadas.

Regra - 2.10:
Cada arquivo fonte deve sempre incluir (#include) o arquivo de cabeçalho do mesmo nome (e.g., o arquivo adc.c deve incluir o adc.h), para permitir que o compilador confirme que cada função pública corresponde com o seu protótipo.

Regra - 2.11:
Os caminhos completos não devem ser usados em nomes de arquivos de #include.

Regra - 2.12:
Cada arquivo fonte deve estar livre de arquivos #include que não são usados.

Regra - 2.13:
Nenhum arquivo fonte deve incluir (#include) outro arquivo fonte (.c)

Razão:
O objetivo e o layout interno de um módulo de arquivo fonte deve ser claro para todos que os mantêm. Por exemplo, as funções públicas são geralmente a de maior interesse e desta forma aparecem acima das funções privadas que elas chamam. De suma importância é que o compilador ache o protótipo para cada função.

Arquivos modelos (templates):
Regra - 2.14:
Um conjunto de modelos para os arquivos de cabeçalho (.h) e fonte (.c) deverão ser mantidos no servidor.

Razão:
Iniciar cada novo arquivo a partir de um modelo garante consistencia nos blocos de comentários dos arquivos de cabeçalho e garante a inclusão de avisos apropriados de direitos autorais.


***
## Notas
1. <a name="IdFootnote01"></a>Ver: LEI Nº 9.609 , DE 19 DE FEVEREIRO DE 1998. Art. 4º - http://www.planalto.gov.br/ccivil_03/leis/l9609.htm
2. <a name="IdFootnote02"></a>Este padrão de codificação prioriza confiabilidade do código acima da eficiência da execução.
3. <a name="IdFootnote03"></a>Os compiladores compatíveis com C99 oferecem muitas melhorias valiosas em relação aos compiladores mais antigos, como comentários no estilo C++, tipos booleanos e inteiros de largura fixa, funções inline e declarações de variáveis locais em qualquer lugar do corpo da função.
4. <a name="IdFootnote04"></a>Evidências empíricas sugerem que os programadores não familiarizados com a palavra-chave volátil acreditam que o recurso de otimização do compilador é mais prejudicial do que útil e desabilita a otimização. Acreditamos que a grande maioria dos sistemas embarcados contém bugs aguardando a ocorrência devido à falta de palavras-chave voláteis. Esses erros geralmente se manifestam como "falhas" ou somente após alterações em uma base de código "comprovada".