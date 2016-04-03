## VIII. Concurrence
### Grossissez à l'aide du modèle de processus

Tout programme informatique, lorsqu'il s'exécute, est représenté par un ou plusieurs processus. Les applications web ont adopté différentes approches d'exécution de processus. Par exemple, les processus PHP s'exécutent comme des processus fils d'Apache, démarrés à la demande lorsque c'est requis par le volume de requêtes. Les processus Java ont adopté l'approche inverse, avec une machine virtuelle qui fournit un super-processus massif qui réserve un gros bloc de ressources système (processeur et mémoire) au démarrage, et la concurrence est gérée en interne à l'aide de threads. Dans les deux cas, les processus qui tournent sont à peine visibles aux développeurs de l'application.

![La scalabilité est exprimée par des processus qui s'exécutent, la diversité de la charge de travail est exprimée par les types de processus](/images/process-types.png)

**Dans une application 12 facteurs, les processus sont des élèves modèles**. Les processus dans une application 12 facteurs s'inspirent fortement du [modèle de processus unix pour faire fonctionner les daemon (en)](http://adam.heroku.com/past/2011/5/9/applying_the_unix_process_model_to_web_apps/). En utilisant ce modèle, les développeurs peuvent structurer l'application pour gérer différents types de charge en assignant chaque type de travail à un *type de processus*. Par exemple, les requêtes HTTP peuvent être gérées par un processus web, et les tâches d'arrière plan ayant une longue durée d'exécution peuvent être des processus dits "worker".

Chaque processus peut malgré tout et individuellement, gérer son propre multiplexage interne, avec des threads à l'intérieur de la machine virtuelle d'exécution, ou à l'aide du modèle d'évènements asynchrone que l'on retrouve dans des outils comme [EventMachine](http://rubyeventmachine.com/), [Twisted](http://twistedmatrix.com/trac/), ou [Node.js](http://nodejs.org/). Mais une machine virtuelle a individuellement une taille limitée (grandissement vertical), donc l'application doit également pouvoir déclencher plusieurs processus qui tournent sur plusieurs machines physiques.

Le modèle de processus prend de l'envergure dès qu'il est question de grossir. La [nature sans partage, avec une partition horizontale des processus des applications 12 facteurs](./processes) signifie qu'ajouter plus de concurrence est une opération simple et fiable. La liste des types de processus et le nombre de processus de chaque type est appelée *formation de processus*.

Les processus des applications 12 facteurs ne devraient [jamais être des daemons (en)](http://dustin.github.com/2010/02/28/running-processes.html) ou écrire des fichiers PID. A la place, utilisez le gestionnaire de processus du système d'exploitation (tel qu'[Upstart](http://upstart.ubuntu.com/), un gestionnaire de processus distribué sur une plateforme cloud, ou un outil comme [Foreman (en)](http://blog.daviddollar.org/2011/05/06/introducing-foreman.html) durant le développement) pour gérer les [flux de sortie](./logs), répondre à un processus qui plante, et gérer les redémarrages et les arrêts initiés par les utilisateurs.