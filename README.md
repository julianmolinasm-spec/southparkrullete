# import { useState, useEffect } from "react";

const EPISODES = [
  { id:1,   title:"Cartman Gets an Anal Probe", s:1,  e:1,  funny:8.2, dark:3, impact:9,  auto:true,  chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","clásico"], desc:"El episodio piloto. Cartman es abducido por aliens y los chicos intentan traer de vuelta a Ike.", why:"El punto de partida de una de las series más influyentes de la historia. Cartman ya era Cartman desde el minuto uno." },
  { id:2,   title:"Weight Gain 4000", s:1,  e:2,  funny:7.8, dark:3, impact:7,  auto:true,  chars:["Cartman","Stan","Kyle"], types:["absurdo","personaje"], desc:"Cartman gana un concurso de redacción. Mr. Garrison planea asesinar a Kathie Lee Gifford.", why:"La dinámica entre Mr. Hat y Garrison ya funciona perfecto. Cartman engordando para ser musculoso es un clásico." },
  { id:3,   title:"Big Gay Al's Big Gay Boat Ride", s:1,  e:4,  funny:8.0, dark:2, impact:8,  auto:true,  chars:["Stan"], types:["político","parodia"], desc:"El perro de Stan resulta ser gay. Stan lo lleva a Big Gay Al's Big Gay Animal Sanctuary.", why:"Episodio pionero en representación positiva gay en TV. Más progresista que la mayoría de los programas de la época." },
  { id:4,   title:"Mr. Hankey the Christmas Poo", s:1,  e:10, funny:8.3, dark:3, impact:9,  auto:true,  chars:["Kyle","Mr.Hankey"], types:["absurdo","clásico"], desc:"Kyle tiene como amigo imaginario a un excremento navideño que habla. Nadie más lo puede ver.", why:"Introduce a Mr. Hankey. La premisa es ridícula y funciona perfectamente." },
  { id:5,   title:"Mecha-Streisand", s:1,  e:12, funny:8.4, dark:3, impact:8,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","parodia"], desc:"Barbra Streisand se convierte en un mecha robot. Robert Smith de The Cure la combate.", why:"Uno de los primeros ataques grandes a una celebridad. El tono absurdo de kaiju es perfecto." },
  { id:6,   title:"Cartman's Mom is a Dirty Slut", s:1,  e:13, funny:8.5, dark:4, impact:8,  auto:true,  chars:["Cartman"], types:["personaje","absurdo"], desc:"Cartman quiere saber quién es su padre. El episodio termina en un cliffhanger brutal.", why:"El inicio del misterio del padre de Cartman que se convirtió en un clásico de la TV." },
  { id:7,   title:"Cartman's Mom is Still a Dirty Slut", s:2, e:2, funny:8.4, dark:4, impact:8, auto:true, chars:["Cartman"], types:["personaje","absurdo"], desc:"Se revela quién es el padre de Cartman. La respuesta es completamente absurda.", why:"El payoff del cliffhanger de S1 es inesperado y gracioso. Establece la lore de Cartman." },
  { id:8,   title:"Gnomes", s:2,  e:17, funny:8.3, dark:2, impact:9,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","político"], desc:"Los chicos investigan gnomos que roban calzoncillos con un plan de negocios incomprensible.", why:"Underpants Gnomes es una de las referencias más longevas de la cultura pop." },
  { id:9,   title:"Chef's Salty Chocolate Balls", s:2, e:9, funny:8.3, dark:2, impact:7, auto:true, chars:["Chef","Mr.Hankey"], types:["absurdo","musical"], desc:"El festival de cine llega a South Park. Mr. Hankey es amenazado por el snob de Hollywood.", why:"La canción de Chef es absolutamente horrible y brillante. Sátira del festival de cine." },
  { id:10,  title:"Chickenpox", s:2,  e:10, funny:8.0, dark:5, impact:7,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["dark","personaje"], desc:"Los padres infectan a los chicos con varicela deliberadamente. Se muestra la pobreza de Kenny.", why:"Una de las primeras veces que muestra la situación de Kenny con seriedad real." },
  { id:11,  title:"City on the Edge of Forever", s:2, e:7, funny:8.2, dark:4, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","meta"], desc:"Los chicos quedan atrapados en el borde de un precipicio. Stan recuerda episodios anteriores... pero todos están mal.", why:"Episodio de clip show que parodia los clip shows siendo creativamente deshonesto. Muy meta para la época." },
  { id:12,  title:"Sexual Harassment Panda", s:3, e:6, funny:8.6, dark:3, impact:8, auto:true, chars:["Cartman","Stan","Kyle"], types:["absurdo","político"], desc:"Un panda enseña sobre acoso sexual en el colegio. Cartman demanda a todo el mundo.", why:"Sátira de la cultura de demandas corporativas con el absurdo del panda. Clásico total." },
  { id:13,  title:"Chinpokomon", s:3,  e:10, funny:8.7, dark:3, impact:8,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","político"], desc:"Una fiebre de Pokémon japonés conquista a los niños. Oculta un plan de control mental.", why:"Parodia perfecta de la fiebre Pokémon con crítica cultural afilada." },
  { id:14,  title:"Tweek vs. Craig", s:3,  e:5,  funny:8.3, dark:3, impact:7,  auto:true,  chars:["Tweek","Craig"], types:["personaje","absurdo"], desc:"Los chicos enfrentan a Tweek y Craig en una pelea. Ambos no tienen interés en pelear.", why:"Introduce la dinámica Tweek-Craig que décadas después se convierte en algo totalmente distinto." },
  { id:15,  title:"Korn's Groovy Pirate Ghost Mystery", s:3, e:12, funny:7.9, dark:5, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","absurdo"], desc:"Korn aparece y resuelven un misterio estilo Scooby-Doo de fantasmas piratas.", why:"Absurdo total con la participación real de Korn. Episodio de Halloween peculiar y querido." },
  { id:16,  title:"Timmy 2000", s:4,  e:3,  funny:8.4, dark:3, impact:7,  auto:true,  chars:["Timmy"], types:["personaje","absurdo"], desc:"Todos diagnostican ADD. Timmy se vuelve una rock star. Phil Collins aparece.", why:"Crítica mordaz al sobrediagnóstico de ADD en niños. Timmy es puro carisma." },
  { id:17,  title:"Cartman Joins NAMBLA", s:4,  e:5,  funny:8.8, dark:7, impact:9,  auto:true,  chars:["Cartman","Kenny"], types:["personaje","dark"], desc:"Cartman busca amigos maduros online y se infiltra en una org de pedófilos sin entender nada.", why:"El remate final es legendario. Kenny tiene un subplot paralelo escalando absurdamente." },
  { id:18,  title:"Fat Camp", s:4,  e:15, funny:8.5, dark:4, impact:7,  auto:true,  chars:["Cartman"], types:["personaje","absurdo"], desc:"Cartman va a un campamento para adelgazar. Kenny hace cosas degradantes por dinero.", why:"El subplot de Kenny es genuinamente perturbador y gracioso al mismo tiempo." },
  { id:19,  title:"Kenny Dies", s:5,  e:13, funny:7.2, dark:9, impact:9,  auto:true,  chars:["Kenny","Cartman","Stan","Kyle"], types:["dark","personaje"], desc:"Kenny muere de verdad de una enfermedad terminal. Esta vez no vuelve. Cartman usa su enfermedad para su propio beneficio.", why:"El episodio más emotivo de las temporadas clásicas. Genuinamente triste." },
  { id:20,  title:"Scott Tenorman Must Die", s:5,  e:4,  funny:9.6, dark:9, impact:10, auto:true,  chars:["Cartman"], types:["personaje","dark"], desc:"Cartman es estafado por un adolescente y planea la venganza más oscura de toda la serie.", why:"El twist final redefinió a Cartman como villano genuino. Impactante e icónico." },
  { id:21,  title:"Towelie", s:5,  e:8,  funny:8.5, dark:3, impact:8,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo"], desc:"Una toalla drogadicta aparece en la vida de los chicos mientras buscan su videojuego.", why:"Absurdismo puro. Towelie es uno de los personajes más queridos del fandom." },
  { id:22,  title:"Cartmanland", s:5,  e:6,  funny:9.5, dark:4, impact:9,  auto:true,  chars:["Cartman","Kyle"], types:["personaje","absurdo"], desc:"Cartman hereda un millón de dólares y compra un parque de diversiones solo para él. Su felicidad se destruye sola.", why:"Ver a Cartman sabotearse por pura avaricia es satisfacción pura." },
  { id:23,  title:"Super Best Friends", s:5,  e:3,  funny:8.5, dark:4, impact:8,  auto:true,  chars:["Stan","Kyle"], types:["parodia","absurdo"], desc:"Los superhéroes de las religiones del mundo se unen para combatir a David Blaine.", why:"Parodia de religiones mundiales que solo SP se atrevería a hacer." },
  { id:24,  title:"Butters' Very Own Episode", s:5, e:14, funny:8.9, dark:8, impact:8, auto:true, chars:["Butters"], types:["dark","personaje"], desc:"Butters descubre un secreto perturbador sobre su padre. Sus padres reaccionan de forma aún más perturbadora.", why:"Butters como protagonista absoluto. El final es brillantemente oscuro." },
  { id:25,  title:"Osama Bin Laden Has Farty Pants", s:5, e:9, funny:8.2, dark:5, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["político","absurdo"], desc:"Los chicos reciben una cabra de Afganistán. Cartman se enfrenta a Bin Laden al estilo Looney Tunes.", why:"Hecho semanas después del 9/11. La valentía de publicarlo entonces es casi inimaginable." },
  { id:26,  title:"Professor Chaos", s:6,  e:6,  funny:9.0, dark:4, impact:8,  auto:true,  chars:["Butters","Cartman"], types:["personaje","absurdo"], desc:"Butters adopta la identidad villana de Professor Chaos. Los chicos buscan su nuevo cuarto amigo.", why:"El origen de Professor Chaos. Butters como supervillano es adorable y absurdo a la vez." },
  { id:27,  title:"The Simpsons Already Did It", s:6, e:7, funny:8.4, dark:3, impact:8, auto:true, chars:["Cartman","Butters"], types:["meta","absurdo"], desc:"Cartman planea el mal pero cada idea ya la hicieron Los Simpsons.", why:"Meta-comedia brillante sobre creatividad e influencia cultural." },
  { id:28,  title:"Red Hot Catholic Love", s:6, e:8, funny:8.4, dark:6, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["político","absurdo"], desc:"Los chicos investigan el abuso clerical. Descubren que puedes comer por el recto.", why:"Sátira de los escándalos de la iglesia mezclada con el absurdo más puro de la serie." },
  { id:29,  title:"Return of the Fellowship", s:6, e:13, funny:8.9, dark:3, impact:8, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","absurdo"], desc:"Los chicos deben devolver una cinta de LOTR a Butters. Era un porno. Todo escala a una épica quest.", why:"Parodia inteligente de Tolkien con humor completamente absurdo." },
  { id:30,  title:"My Future Self n' Me", s:6, e:16, funny:8.5, dark:4, impact:7, auto:true, chars:["Stan","Cartman"], types:["absurdo","personaje"], desc:"Los padres de Stan contratan a un actor para que sea su 'yo del futuro' drogadicto y fracasado.", why:"El plan de Cartman para exponer a todos los padres que hacen lo mismo es ingenioso y gracioso." },
  { id:31,  title:"Cancelled", s:7, e:1, funny:8.7, dark:3, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["meta","absurdo"], desc:"La Tierra es en realidad un reality show intergaláctico y lo están por cancelar.", why:"La premisa meta de que la Tierra es un programa de TV es brillante." },
  { id:32,  title:"Fat Butt and Pancake Head", s:7, e:5, funny:8.8, dark:4, impact:8, auto:true, chars:["Cartman"], types:["personaje","absurdo"], desc:"Cartman hace que su mano sea Jennifer Lopez. La mano adquiere vida propia. Ben Affleck se enamora de ella.", why:"Cartman siendo ventrílocuo de sí mismo para trollear a Kyle es puro genio." },
  { id:33,  title:"Lil' Crime Stoppers", s:7, e:6, funny:8.7, dark:5, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","absurdo"], desc:"Los chicos juegan a ser policías del parque. El episodio escala a una película de acción policial seria.", why:"La transición de juego infantil a thriller de acción adulto es perfectamente ejecutada." },
  { id:34,  title:"Christian Rock Hard", s:7, e:9, funny:8.8, dark:3, impact:8, auto:true, chars:["Cartman","Kyle"], types:["personaje","parodia"], desc:"Cartman apuesta contra Kyle que puede hacer un disco de platino con una banda de rock cristiano.", why:"Cartman siendo un genio del marketing de la peor manera posible." },
  { id:35,  title:"Casa Bonita", s:7,  e:11, funny:9.0, dark:5, impact:9,  auto:true,  chars:["Cartman","Butters"], types:["personaje","dark"], desc:"Cartman convence a Butters de esconderse del apocalipsis para ir a Casa Bonita en su lugar.", why:"Cartman en modo maquiavélico por razones completamente estúpidas." },
  { id:36,  title:"All About Mormons", s:7, e:12, funny:8.9, dark:3, impact:9, auto:true, chars:["Stan"], types:["político","parodia"], desc:"Una familia mormona se muda a South Park. Los flashbacks musicales narran la historia de Joseph Smith.", why:"Sátira respetuosa pero afilada del mormonismo. Dum dum dum dum dum..." },
  { id:37,  title:"Raisins", s:7,  e:14, funny:8.6, dark:7, impact:7,  auto:true,  chars:["Stan","Butters"], types:["personaje","dark"], desc:"Stan es abandonado por Wendy. Butters se enamora de una chica de un Hooters para niños.", why:"El arco gótico de Stan es memorable. El de Butters es inesperadamente conmovedor." },
  { id:38,  title:"Good Times with Weapons", s:8, e:1, funny:8.6, dark:5, impact:8, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Butters"], types:["parodia","absurdo"], desc:"Los chicos compran armas ninja y se imaginan guerreros de anime. Butters sufre accidentalmente.", why:"El segmento animado en estilo anime es visualmente increíble." },
  { id:39,  title:"AWESOM-O", s:8,  e:5,  funny:9.1, dark:3, impact:9,  auto:true,  chars:["Cartman","Butters"], types:["personaje","absurdo"], desc:"Cartman se disfraza de robot para espiar a Butters. El plan se sale de control totalmente.", why:"Butters siendo adorable vs Cartman sufriendo las consecuencias. Perfecto." },
  { id:40,  title:"Douche and Turd", s:8, e:8, funny:8.5, dark:4, impact:8, auto:true, chars:["Stan","Kyle"], types:["político","absurdo"], desc:"La mascota del colegio se reemplaza. Los candidatos son una Douche y un Turd Sandwich.", why:"Sátira electoral perfecta sobre votar por el mal menor." },
  { id:41,  title:"Goobacks", s:8,  e:7,  funny:8.6, dark:5, impact:8,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["político","absurdo"], desc:"Inmigrantes del futuro llegan al presente porque en el futuro no hay trabajo.", why:"Sátira de la inmigración usando viajeros del tiempo. La solución que propone el pueblo es ridícula." },
  { id:42,  title:"Woodland Critter Christmas", s:8, e:14, funny:9.2, dark:9, impact:9, auto:true, chars:["Cartman"], types:["dark","absurdo"], desc:"Cartman narra un cuento navideño sobre criaturas del bosque que resultan ser satánicas.", why:"El giro es completamente inesperado y brillante. Oscuro de una forma que solo SP puede lograr." },
  { id:43,  title:"Pre-School", s:8,  e:10, funny:8.5, dark:7, impact:7,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["dark","absurdo"], desc:"Un chico aterrador que quemaron de preescolar sale de la cárcel y busca venganza.", why:"Parodia de las pelis de presos vengadores ambientada en preescolar." },
  { id:44,  title:"Cartman's Incredible Gift", s:8, e:13, funny:8.6, dark:5, impact:7, auto:true, chars:["Cartman","Kyle"], types:["personaje","absurdo"], desc:"Cartman se cae y cree que tiene poderes psíquicos. Los usa para resolver crímenes. La policía le cree.", why:"Cartman inventando 'visiones' y engañando a toda la policía de South Park es brillante." },
  { id:45,  title:"Die Hippie Die", s:9,  e:3,  funny:8.8, dark:3, impact:8,  auto:true,  chars:["Cartman"], types:["personaje","absurdo"], desc:"Cartman es el único capaz de combatir la invasión hippie de South Park. Necesita un taladro y Slayer.", why:"Cartman como heroico cazador de hippies es absolutamente glorioso." },
  { id:46,  title:"Best Friends Forever", s:9, e:4, funny:8.7, dark:6, impact:8, auto:true, chars:["Kenny","Cartman","Stan","Kyle"], types:["dark","parodia"], desc:"Kenny muere y llega al cielo. En la Tierra, todos pelean por su consola de juegos como si fuera Terri Schiavo.", why:"Parodia del caso Terri Schiavo hecha mientras el caso ocurría. Audacia máxima." },
  { id:47,  title:"The Losing Edge", s:9,  e:5,  funny:9.0, dark:2, impact:8,  auto:true,  chars:["Randy","Stan"], types:["absurdo","personaje"], desc:"Los chicos intentan perder béisbol todo el verano. Randy se pelea borracho con padres de otros equipos.", why:"Randy Marsh en su forma más gloriosa e irresponsable." },
  { id:48,  title:"The Death of Eric Cartman", s:9, e:6, funny:8.8, dark:3, impact:8, auto:true, chars:["Cartman","Butters"], types:["personaje","absurdo"], desc:"Los chicos deciden ignorar a Cartman. Él cree que murió. Butters lo ayuda a 'resolver asuntos pendientes'.", why:"La dinámica Cartman-Butters en su punto más gracioso y absurdo." },
  { id:49,  title:"Ginger Kids", s:9,  e:11, funny:8.6, dark:6, impact:8,  auto:true,  chars:["Cartman","Kyle"], types:["personaje","dark"], desc:"Cartman lanza un discurso de odio contra los pelirrojos. Luego se convierte en uno.", why:"La ironía del final es perfecta. Cartman víctima de su propia campaña." },
  { id:50,  title:"Trapped in the Closet", s:9,  e:12, funny:9.3, dark:3, impact:10, auto:true,  chars:["Stan"], types:["parodia","político"], desc:"Stan es declarado reencarnación de L. Ron Hubbard. Tom Cruise se encierra en un clóset.", why:"Sátira despiadada de Cienciología que requirió valentía real." },
  { id:51,  title:"Free Willzyx", s:9,  e:13, funny:8.5, dark:2, impact:7,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo"], desc:"Los chicos creen que una orca del acuario es un alienígena que quiere volver a la Luna.", why:"La lógica completamente absurda llevada hasta sus últimas consecuencias." },
  { id:52,  title:"Marjorine", s:9,  e:9,  funny:9.0, dark:7, impact:8,  auto:true,  chars:["Butters"], types:["personaje","absurdo"], desc:"Butters se disfraza de niña para infiltrarse en una pijamada femenina. Sus padres creen que está muerto.", why:"Butters cross-dressing con absoluta inocencia. Sus padres tienen la reacción más oscura e inesperada." },
  { id:53,  title:"The Return of Chef", s:10, e:1,  funny:8.5, dark:8, impact:9,  auto:true,  chars:["Chef","Stan","Kyle","Cartman","Kenny"], types:["dark","personaje"], desc:"Chef vuelve a South Park completamente cambiado tras unirse a una organización secreta.", why:"Oscuro por las circunstancias reales detrás del episodio. Uno de los más memorables emocionalmente." },
  { id:54,  title:"Cartoon Wars", s:10, e:3,  funny:9.0, dark:5, impact:9,  auto:false, chars:["Cartman","Kyle"], types:["político","meta"], desc:"Cartman y Kyle compiten para decidir si Family Guy debe censurar a Mahoma. La pelea sobre libertad de expresión es real.", why:"Meta-comentario sobre la libertad de expresión justo cuando el tema era candente. Valiente." },
  { id:55,  title:"ManBearPig", s:10, e:6,  funny:8.7, dark:4, impact:9,  auto:true,  chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","político"], desc:"Al Gore visita South Park convencido de que ManBearPig es una amenaza real. Nadie le cree.", why:"La parodia de Al Gore y el alarmismo climático. Envejeció muy bien con el tiempo." },
  { id:56,  title:"Make Love, Not Warcraft", s:10, e:8,  funny:9.8, dark:2, impact:10, auto:true,  chars:["Cartman","Stan","Kyle","Kenny"], types:["parodia","absurdo"], desc:"Los chicos farmean WoW para derrotar a un griefer de nivel imposible.", why:"Animaciones reales de WoW mezcladas con SP. Un ícono absoluto de internet y gaming." },
  { id:57,  title:"Go God Go", s:10, e:12, funny:8.8, dark:4, impact:8,  auto:false, chars:["Cartman","Kyle"], types:["absurdo","político"], desc:"Cartman se congela esperando la Wii. El futuro sin religión tiene guerras entre facciones ateas.", why:"Sátira del dogmatismo ateo tan buena como la del religioso. La Wii como macguffin es perfecta." },
  { id:58,  title:"With Apologies to Jesse Jackson", s:11, e:1, funny:8.6, dark:6, impact:8, auto:true, chars:["Randy","Stan"], types:["político","absurdo"], desc:"Randy dice una palabra en Wheel of Fortune y no entiende por qué todos están ofendidos.", why:"Randy completamente ajeno al caos que causó. Uno de sus mejores episodios." },
  { id:59,  title:"Night of the Living Homeless", s:11, e:7, funny:8.7, dark:5, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["parodia","político"], desc:"South Park es invadido por personas sin hogar que solo dicen 'change'. Parodia de zombies.", why:"Parodia de película de zombies con los sin techo. Incómoda pero muy bien ejecutada." },
  { id:60,  title:"Le Petit Tourette", s:11, e:8,  funny:8.8, dark:6, impact:8,  auto:true,  chars:["Cartman"], types:["personaje","dark"], desc:"Cartman finge Tourette's para insultar a todos sin consecuencias. Luego pierde el control del tic.", why:"El plan le explota en la cara de la forma más satisfactoria posible." },
  { id:61,  title:"Imaginationland", s:11, e:10, funny:8.7, dark:6, impact:9,  auto:false, chars:["Cartman","Kyle","Butters"], types:["parodia","épico"], desc:"Trilogía completa: terroristas atacan Imaginationland. Los personajes de fantasía cobran vida. Kyle tiene una deuda.", why:"La trilogía más ambiciosa del show con referencias a todo el universo pop cultural. Muy ambicioso." },
  { id:62,  title:"Guitar Queer-O", s:11, e:13, funny:8.5, dark:4, impact:7,  auto:true,  chars:["Stan","Kyle"], types:["parodia","personaje"], desc:"Stan y Kyle se vuelven adictos a Guitar Hero. El éxito los separa.", why:"Parodia perfecta de rockstar biopics usando Guitar Hero como metáfora." },
  { id:63,  title:"The List", s:11, e:14, funny:8.8, dark:6, impact:8,  auto:true,  chars:["Kyle","Cartman","Stan"], types:["personaje","absurdo"], desc:"Las chicas tienen una lista secreta de quiénes son los chicos más lindos del grado. Kyle queda último.", why:"El espiral de consecuencias a partir de una lista escolar es perfectamente construido." },
  { id:64,  title:"Tonsil Trouble", s:12, e:1,  funny:8.5, dark:6, impact:7,  auto:true,  chars:["Cartman","Kyle"], types:["personaje","dark"], desc:"Cartman adquiere HIV accidentalmente. Inmediatamente infecta a Kyle. Se van a buscar a Magic Johnson.", why:"Cartman infectando a Kyle con HIV es uno de sus actos más bajos. Y aún así es hilarante." },
  { id:65,  title:"Britney's New Look", s:12, e:2, funny:8.0, dark:8, impact:8, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["político","dark"], desc:"Los chicos explotan la crisis mental de Britney Spears. La sociedad la usa como chivo expiatorio.", why:"Una de las críticas más oscuras al culture del espectáculo. El final es perturbadoramente bíblico." },
  { id:66,  title:"Major Boobage", s:12, e:3,  funny:8.4, dark:4, impact:7,  auto:true,  chars:["Kenny","Randy"], types:["parodia","absurdo"], desc:"Los chicos se drogan inhalando gases de gato. Kenny viaja a una dimensión de heavy metal.", why:"Parodia hermosa de Heavy Metal (1981). Visualmente uno de los más creativos." },
  { id:67,  title:"Over Logging", s:12, e:6,  funny:8.8, dark:5, impact:8,  auto:true,  chars:["Randy","Stan"], types:["absurdo","parodia"], desc:"El internet desaparece de repente. Randy está dispuesto a cruzar el país entero para encontrarlo.", why:"Sátira de la adicción a internet que se volvió más relevante con los años, no menos." },
  { id:68,  title:"Breast Cancer Show Ever", s:12, e:9, funny:8.7, dark:6, impact:8, auto:true, chars:["Cartman","Wendy"], types:["personaje","absurdo"], desc:"Cartman se burla del cáncer de mama y Wendy decide golpearlo después del colegio.", why:"Ver a Cartman aterrorizado durante todo el episodio es una satisfacción enorme." },
  { id:69,  title:"About Last Night...", s:12, e:12, funny:8.6, dark:3, impact:7, auto:true, chars:["Stan","Kyle","Randy"], types:["político","absurdo"], desc:"Obama gana las elecciones. Una facción celebra histéricamente. La otra llora. Hay un heist dentro de todo.", why:"Salió el día DESPUÉS de la elección de Obama 2008. Velocidad de producción legendaria." },
  { id:70,  title:"The Ungroundable", s:12, e:14, funny:8.4, dark:3, impact:6, auto:true, chars:["Butters"], types:["personaje","parodia"], desc:"Butters cree que es un vampiro. Los góticos están indignados de que los confundan con los vampiro-emo.", why:"Parodia del fenómeno Twilight perfectamente ejecutada. Butters como vampiro es encantador." },
  { id:71,  title:"The Ring", s:13, e:1,  funny:8.4, dark:4, impact:7,  auto:true,  chars:["Kenny"], types:["parodia","absurdo"], desc:"Kenny sale con una chica que usa un anillo de castidad de los Jonas Brothers. Disney manipula sexualmente a los adolescentes.", why:"Crítica frontal a Disney y los Jonas Brothers como herramientas de control." },
  { id:72,  title:"Margaritaville", s:13, e:3,  funny:9.0, dark:4, impact:9,  auto:true,  chars:["Randy","Kyle","Cartman"], types:["político","parodia"], desc:"La crisis económica del 2008 es culpa de los que gastan demasiado. Randy predica austeridad total.", why:"Hecho durante la crisis financiera. Kyle como Jesucristo económico es brillante." },
  { id:73,  title:"Fishsticks", s:13, e:5,  funny:9.2, dark:2, impact:9,  auto:true,  chars:["Cartman","Jimmy"], types:["personaje","absurdo"], desc:"Jimmy inventa el chiste más gracioso del mundo. Cartman convence a todos de que fue él. Kanye no lo entiende.", why:"Kanye West teniendo una crisis existencial por un chiste de peces es perfecto." },
  { id:74,  title:"Whale Whores", s:13, e:11, funny:8.7, dark:5, impact:7,  auto:true,  chars:["Stan","Randy"], types:["parodia","político"], desc:"Stan se une a un barco de Sea Shepherd para proteger ballenas. Randy tiene una banda de death metal.", why:"Parodia de Whale Wars con un giro histórico completamente inesperado y ridículo." },
  { id:75,  title:"The Tale of Scrotie McBoogerballs", s:14, e:2, funny:8.6, dark:5, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Butters"], types:["meta","absurdo"], desc:"Los chicos escriben el libro más asqueroso del mundo y se convierte en un bestseller. Todo el mundo ve mensajes profundos en él.", why:"Crítica brillante a la proyección de significado en arte intencional y deliberadamente vacío." },
  { id:76,  title:"Medicinal Fried Chicken", s:14, e:3, funny:8.8, dark:4, impact:8, auto:true, chars:["Cartman","Randy"], types:["absurdo","personaje"], desc:"KFC es reemplazado por dispensarios de marihuana. Cartman construye un cartel del pollo frito. Randy se droga.", why:"Dos subplots brillantes corriendo en paralelo. Cartman como Scarface del KFC es perfecto." },
  { id:77,  title:"You Have 0 Friends", s:14, e:4,  funny:8.9, dark:3, impact:8,  auto:true,  chars:["Stan","Kyle"], types:["parodia","absurdo"], desc:"Stan se vuelve adicto a Facebook. Kyle queda atrapado dentro del videojuego de Facebook.", why:"Tron dentro de Facebook. El absurdo llega a niveles épicos y la sátira sigue vigente." },
  { id:78,  title:"200", s:14, e:5,  funny:9.0, dark:5, impact:9,  auto:false, chars:["Cartman","Stan","Kyle","Kenny","Randy"], types:["meta","épico"], desc:"Episodio 200 de la serie. Todas las celebridades demandadas se unen. Regresan muchos personajes.", why:"Celebración masiva de la historia del show. Fan service del bueno." },
  { id:79,  title:"Crème Fraîche", s:14, e:14, funny:8.7, dark:5, impact:7,  auto:true,  chars:["Randy","Stan"], types:["absurdo","personaje"], desc:"Randy se vuelve adicto al porno de cocina. Stan intenta integrar a Butters al colegio.", why:"El subplot de Butters y la máquina de ejercicio es absolutamente hilariante." },
  { id:80,  title:"HumancentiPad", s:15, e:1,  funny:8.6, dark:8, impact:8,  auto:true,  chars:["Cartman","Kyle","Randy"], types:["dark","parodia"], desc:"Kyle acepta los términos y condiciones de iTunes sin leerlos. Las consecuencias son perturbadoras.", why:"El paralelo entre las condiciones de iTunes y The Human Centipede es brillante y oscuro." },
  { id:81,  title:"Crack Baby Athletic Association", s:15, e:5, funny:8.7, dark:8, impact:8, auto:true, chars:["Cartman","Kyle"], types:["dark","personaje","político"], desc:"Cartman crea una liga deportiva de bebés adictos al crack y la monetiza.", why:"Sátira oscura de la explotación deportiva. Incómodamente gracioso." },
  { id:82,  title:"You're Getting Old", s:15, e:7,  funny:7.8, dark:9, impact:9,  auto:true,  chars:["Stan"], types:["dark","personaje"], desc:"Stan cumple 10 años y empieza a percibir todo como literal mierda. Una de las más oscuras.", why:"Más emotiva que graciosa. Honesta sobre lo que es crecer y perder el entusiasmo." },
  { id:83,  title:"1%", s:15, e:12, funny:8.5, dark:6, impact:7, auto:true, chars:["Cartman","Stan"], types:["político","personaje"], desc:"El colegio tiene los peores resultados físicos del país. Cartman culpa al 1% por todo.", why:"Sátira del movimiento Occupy Wall Street con Cartman siendo el 1% más egocéntrico posible." },
  { id:84,  title:"Broadway Bro Down", s:15, e:11, funny:8.4, dark:5, impact:7, auto:true, chars:["Randy","Stan"], types:["absurdo","parodia"], desc:"Randy descubre que los musicales de Broadway son básicamente publicidades de sexo oral.", why:"La conspiración de los musicales es una de las teorías más ridículas y bien ejecutadas del show." },
  { id:85,  title:"Cash For Gold", s:16, e:2,  funny:8.6, dark:7, impact:7,  auto:true,  chars:["Cartman","Stan"], types:["político","absurdo"], desc:"Cartman lanza un canal de teletienda para joyería. El abuelo de Stan regala lo que le venden.", why:"Crítica al ciclo de explotación de adultos mayores que es completamente deprimente y gracioso." },
  { id:86,  title:"Sarcastaball", s:16, e:8,  funny:8.6, dark:5, impact:7,  auto:true,  chars:["Randy","Stan"], types:["político","absurdo"], desc:"Randy propone sarcásticamente un deporte seguro. Todos lo toman en serio.", why:"Randy destruyendo el deporte americano por accidente. Uno de sus mejores arcos." },
  { id:87,  title:"A Nightmare on Face Time", s:16, e:12, funny:8.6, dark:5, impact:7, auto:true, chars:["Randy","Stan"], types:["parodia","absurdo"], desc:"Randy compra un Blockbuster y enloquece al estilo The Shining. Los chicos van de Halloween a través de FaceTime.", why:"Parodia de The Shining usando el funeral de Blockbuster como escenario. Perfectamente ejecutada." },
  { id:88,  title:"Informative Murder Porn", s:17, e:2, funny:8.7, dark:5, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["parodia","político"], desc:"Los padres se vuelven adictos a los programas de crímenes reales. Los chicos los bloquean con Minecraft.", why:"Los hijos bloqueando a sus padres de programas violentos es una inversión perfecta de la realidad." },
  { id:89,  title:"Black Friday", s:17, e:7,  funny:9.1, dark:5, impact:9,  auto:false, chars:["Cartman","Stan","Kyle","Kenny","Randy"], types:["parodia","épico"], desc:"La trilogía de Game of Thrones ambientada en el Black Friday de un mall. Cartman lidera una facción.", why:"La parodia de GoT es increíblemente detallada. Uno de los mejores multi-episodios de la serie." },
  { id:90,  title:"The Hobbit", s:17, e:10, funny:8.7, dark:5, impact:7, auto:true, chars:["Wendy","Cartman","Kyle"], types:["político","parodia"], desc:"Wendy intenta detener que Kim Kardashian sea tratada como sex symbol. Todos en el pueblo usan Photoshop.", why:"Crítica al retoque digital antes de que fuera tema mainstream." },
  { id:91,  title:"The Cissy", s:18, e:3,  funny:8.7, dark:4, impact:7,  auto:true,  chars:["Cartman","Randy","Stan"], types:["político","personaje"], desc:"Cartman finge ser trans para usar el baño de las chicas. Randy resulta ser Lorde.", why:"El giro de Randy siendo Lorde es completamente absurdo y perfecto. La canción es real." },
  { id:92,  title:"Freemium Isn't Free", s:18, e:6, funny:8.8, dark:6, impact:8, auto:true, chars:["Stan","Randy"], types:["político","parodia"], desc:"Stan se vuelve adicto a un juego móvil freemium. El diablo está detrás del modelo de negocio.", why:"Crítica al modelo freemium que sigue siendo perfectamente vigente. El diablo como CEO es genial." },
  { id:93,  title:"Grounded Vindaloop", s:18, e:7,  funny:9.0, dark:4, impact:8,  auto:true,  chars:["Cartman","Butters","Kyle"], types:["absurdo","meta"], desc:"Cartman convence a Butters de que está viviendo en realidad virtual. Nadie sabe qué es real.", why:"Uno de los más inventivos de toda la serie. Las capas de meta-realidad escalan perfectamente." },
  { id:94,  title:"Stunning and Brave", s:19, e:1,  funny:8.7, dark:4, impact:8,  auto:true,  chars:["Cartman","PC Principal"], types:["político","personaje"], desc:"Un nuevo director PC Principal llega al colegio e impone corrección política extrema.", why:"Introduce a PC Principal, uno de los mejores personajes recurrentes de las últimas temporadas." },
  { id:95,  title:"You're Not Yelping", s:19, e:4, funny:8.8, dark:4, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["político","absurdo"], desc:"Cartman y el pueblo se vuelven críticos de Yelp abusivos. Los restaurantes se rebelan.", why:"Sátira de los Yelpers intimidadores que sigue completamente vigente hoy." },
  { id:96,  title:"Tweek x Craig", s:19, e:6,  funny:8.6, dark:2, impact:8,  auto:true,  chars:["Tweek","Craig"], types:["absurdo","parodia"], desc:"Los estudiantes asiáticos crean fanart de yaoi de Tweek y Craig. El colegio entero los trata como pareja.", why:"Tweek y Craig siendo completamente confundidos por la situación es adorable y absurdo." },
  { id:97,  title:"Sponsored Content", s:19, e:8,  funny:9.0, dark:5, impact:9,  auto:false, chars:["Jimmy","Randy"], types:["político","meta"], desc:"Jimmy como editor del periódico escolar descubre que los ads nativos contaminan el periodismo real.", why:"Sátira del contenido patrocinado y los medios que se volvió profética." },
  { id:98,  title:"Member Berries", s:20, e:1,  funny:8.5, dark:4, impact:8,  auto:true,  chars:["Randy","Cartman","PC Principal"], types:["político","absurdo"], desc:"Aparecen las Member Berries, uvas que inducen nostalgia. La temporada serializada comienza.", why:"Introduce las Member Berries, uno de los símbolos más icónicos de la nostalgia pop reciente." },
  { id:99,  title:"White People Renovating Houses", s:21, e:1, funny:8.5, dark:5, impact:7, auto:true, chars:["Randy","Stan"], types:["político","absurdo"], desc:"Los Confederados de South Park son Alexa y los asistentes de voz. Randy hace un show de renovación.", why:"Sátira de la automatización y el desplazamiento laboral usando asistentes de voz." },
  { id:100, title:"Franchise Prequel", s:21, e:4, funny:8.8, dark:4, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny","Butters"], types:["parodia","absurdo"], desc:"Los Coon & Friends quieren que Facebook haga su documental de origen. Mark Zuckerberg los traiciona.", why:"Zuckerberg como villain en un universo de superhéroes es perfecto." },
  { id:101, title:"Dead Kids", s:22, e:1,  funny:8.6, dark:8, impact:8,  auto:true,  chars:["Sharon","Stan","Randy"], types:["político","dark"], desc:"Hay un tiroteo en el colegio de South Park. Sharon es la única que reacciona con alarma. Todos los demás se acostumbraron.", why:"Sátira sobre la normalización de los tiroteos escolares tan oscura que incomoda. Ese es exactamente el punto." },
  { id:102, title:"The Problem with a Poo", s:22, e:3, funny:8.5, dark:6, impact:7, auto:true, chars:["Randy","Mr.Hankey"], types:["político","parodia"], desc:"Mr. Hankey dice cosas inapropiadas en Twitter y es cancelado. Randy produce un musical de Hamilton.", why:"Sátira de la cultura de cancelación usando a Mr. Hankey como víctima inesperada." },
  { id:103, title:"Tegridy Farms", s:22, e:4,  funny:8.5, dark:4, impact:7,  auto:true,  chars:["Randy","Stan"], types:["absurdo","personaje"], desc:"Randy se muda al campo con su familia para cultivar marihuana en Tegridy Farms.", why:"Introduce uno de los arcos más largos de las últimas temporadas. Randy en modo granjero es oro." },
  { id:104, title:"Band in China", s:23, e:2,  funny:8.8, dark:6, impact:9,  auto:true,  chars:["Randy","Stan","Cartman"], types:["político","parodia"], desc:"Randy expande su negocio de marihuana a China. Cartman adapta su historia de vida para Hollywood.", why:"Crítica directa a la autocensura de Hollywood frente al mercado chino. Brutal y muy valiente." },
  { id:105, title:"Shots!!!", s:23, e:3,  funny:8.5, dark:5, impact:7,  auto:true,  chars:["Cartman","Randy","Butters"], types:["político","absurdo"], desc:"Cartman aterroriza a una médica para no recibir vacunas. Randy hace algo aún más irresponsable.", why:"Sátira del movimiento antivacunas que envejeció especialmente bien después de la pandemia." },
  { id:106, title:"The Pandemic Special", s:24, e:1, funny:8.0, dark:4, impact:8, auto:true, chars:["Randy","Stan"], types:["político","parodia"], desc:"Randy podría haber causado el COVID. Los chicos van al colegio con distanciamiento social.", why:"Salió semanas después del inicio de la pandemia. La velocidad de producción es casi increíble." },
  { id:107, title:"South ParQ Vaccination Special", s:24, e:2, funny:8.2, dark:4, impact:7, auto:true, chars:["Randy","PC Principal","Cartman"], types:["político","parodia"], desc:"La gente lucha por conseguir vacunas del COVID. Los profesores del colegio forman QAnon.", why:"QAnon como culto de profesores desesperados por volver al trabajo es un giro genial." },
  { id:108, title:"Pajama Day", s:25, e:1, funny:8.3, dark:4, impact:6, auto:true, chars:["Cartman","PC Principal"], types:["absurdo","personaje"], desc:"Cartman lidera una huelga por poder usar pijamas en el colegio. PC Principal enfrenta una crisis.", why:"Cartman vs PC Principal siempre funciona bien." },
  { id:109, title:"The Big Fix", s:25, e:2,  funny:8.4, dark:5, impact:7,  auto:true,  chars:["Tolkien","Cartman","Stan","Kyle"], types:["político","absurdo"], desc:"Se revela que el nombre del personaje negro siempre fue Tolkien, no Token. Nadie lo había notado.", why:"El giro meta de cambiar el nombre de Token a Tolkien es uno de los más inteligentes recientes." },
  { id:110, title:"City People", s:25, e:4,  funny:8.3, dark:4, impact:6,  auto:true,  chars:["Randy","Stan"], types:["político","absurdo"], desc:"Gente de ciudad se muda a South Park huyendo del COVID. Los locales están divididos.", why:"Sátira de la gentrificación rural post-pandemia. Randy en modo proteccionista es oro." },
  { id:111, title:"Cupid Ye", s:26, e:1,  funny:8.5, dark:5, impact:7,  auto:true,  chars:["Cartman","Kyle"], types:["personaje","absurdo"], desc:"Cartman tiene un amigo imaginario en forma de Kanye West bebé alado y hace declaraciones antisemitas.", why:"La caída de Kanye West convertida en personaje dentro del universo de Cartman es brillante." },
  { id:112, title:"Joining the Panderverse", s:26, e:4, funny:8.6, dark:5, impact:7, auto:true, chars:["Cartman","PC Principal"], types:["político","parodia"], desc:"Cartman tiene pesadillas en las que todos son reemplazados por versiones woke. Parodia de Spider-Verse.", why:"Crítica al 'pandering' de Hollywood usando la estética de Spider-Verse es muy creativo." },
  { id:113, title:"Spookyfish", s:2,  e:15, funny:8.4, dark:5, impact:7,  auto:true,  chars:["Cartman","Stan"], types:["absurdo","parodia"], desc:"Un pez del más allá empieza a matar gente. Aparece un Cartman del universo espejo que es amable.", why:"La inversión del Cartman amable es hilarante. Episodio de Halloween clásico." },
  { id:114, title:"Freak Strike", s:6, e:3, funny:8.3, dark:5, impact:6, auto:true, chars:["Butters","Cartman"], types:["personaje","absurdo"], desc:"Butters se disfraza de fenómeno de circo para ganar en un talk show de Maury Povich. Cartman va al show de Maury.", why:"Butters sufriendo por los planes de Cartman en modo máximo. El segmento de Cartman en Maury es legendario." },
  { id:115, title:"The Coon", s:13, e:2, funny:8.6, dark:4, impact:7, auto:true, chars:["Cartman"], types:["personaje","parodia"], desc:"Cartman se convierte en el superhéroe enmascarado The Coon para hacer justicia.", why:"Cartman como vigilante nocturno es exactamente tan ridículo como suena." },
  { id:116, title:"Put It Down", s:21, e:2, funny:8.6, dark:6, impact:7, auto:true, chars:["Tweek","Craig","Cartman"], types:["político","absurdo"], desc:"Tweek está traumatizado por los tweets de Trump hacia Corea del Norte. Craig intenta calmarlo.", why:"La ansiedad nuclear tratada con ternura en la relación Tweek-Craig." },
  { id:117, title:"Sons A Witches", s:21, e:6, funny:8.5, dark:5, impact:6, auto:true, chars:["Randy","Stan"], types:["absurdo","parodia"], desc:"Los hombres de South Park celebran Halloween bebiendo en el bosque. Uno se convierte en bruja real.", why:"Randy en modo fraternidad de adultos perdidos es súper gracioso. Halloween siempre les queda bien." },
  { id:118, title:"Raising the Bar", s:16, e:9, funny:8.7, dark:5, impact:7, auto:true, chars:["Cartman","Kyle"], types:["político","absurdo"], desc:"Cartman usa un scooter de movilidad por ser gordo. James Cameron baja literalmente el bar en el océano.", why:"El James Cameron real participó. La alegoría sobre bajar los estándares culturales es perfecta." },
  { id:119, title:"Buddha Box", s:22, e:8, funny:8.5, dark:4, impact:6, auto:true, chars:["Cartman","PC Principal"], types:["político","personaje"], desc:"Cartman finge ansiedad social para usar una caja de teléfono en clase. PC Principal también tiene ansiedad.", why:"La caja de Cartman como metáfora del aislamiento digital es más relevante cada año." },
  { id:120, title:"Mexican Joker", s:23, e:1, funny:8.4, dark:7, impact:7, auto:true, chars:["Kyle","Cartman","Randy"], types:["político","dark"], desc:"Kyle visita centros de detención de ICE. Cartman ve la película Joker varias veces.", why:"Dos sátiras simultáneas sobre política migratoria y la glorificación cinematográfica de los incel." },

  // ── S1 extras ──
  { id:121, title:"An Elephant Makes Love to a Pig", s:1, e:5, funny:7.8, dark:4, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo"], desc:"Kyle intenta cruzar su elefante con el cerdo de Cartman. Aparece un clon de Stan que siembra el caos.", why:"Absurdismo clásico de las primeras temporadas. El clon destructor es puro caos infantil." },
  { id:122, title:"Death", s:1, e:6, funny:7.7, dark:6, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["dark","absurdo"], desc:"El abuelo de Stan quiere que lo ayude a morir. La Muerte persigue a Kenny. Los padres protestan contra Terrance y Philip.", why:"Uno de los primeros en explorar temas oscuros reales. La protesta de los padres contra la TV violenta es meta perfecta." },
  { id:123, title:"Pink Eye", s:1, e:7, funny:8.0, dark:5, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","parodia"], desc:"Un accidente en la funeraria convierte a Kenny en zombie. Cartman se disfraza de Hitler para Halloween.", why:"El primer episodio de Halloween. Kenny zombie con Worchestershire sauce es glorioso." },
  { id:124, title:"Starvin' Marvin", s:1, e:9, funny:7.9, dark:5, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","político"], desc:"Los chicos adoptan accidentalmente a un niño etíope. Cartman se confunde con un pavo mutante.", why:"Uno de los primeros episodios políticamente incorrectos. Establece el tono de sátira del hambre en el mundo." },
  { id:125, title:"Tom's Rhinoplasty", s:1, e:11, funny:7.8, dark:4, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Wendy"], types:["personaje","absurdo"], desc:"El señor Garrison se hace una rinoplastia y queda irreconociblemente atractivo. Wendy cela a Stan.", why:"Introduce la dinámica Stan-Wendy. Mr. Garrison como sex symbol es perturbador y gracioso." },

  // ── S2 extras ──
  { id:126, title:"Cartman's Mom: Whodunit Special", s:2, e:3, funny:8.4, dark:4, impact:7, auto:true, chars:["Cartman"], types:["personaje","absurdo"], desc:"El equipo de South Park rompe el cuarto muro para explicar el cliffhanger del padre de Cartman.", why:"El meta-episodio que parodia los propios cliffhangers de la serie. Trey y Matt aparecen como personajes." },
  { id:127, title:"Ike's Wee Wee", s:2, e:4, funny:8.1, dark:3, impact:7, auto:true, chars:["Kyle","Ike","Mr. Mackey"], types:["absurdo","personaje"], desc:"Ike va a ser circuncidado. Kyle lo esconde. Mr. Mackey hace una campaña antidrogas y termina drogándose.", why:"El subplot de Mr. Mackey drogándose es uno de los más graciosos de las primeras temporadas." },
  { id:128, title:"Conjoined Fetus Lady", s:2, e:5, funny:8.0, dark:3, impact:6, auto:true, chars:["Kyle","Stan","Cartman","Kenny"], types:["absurdo","político"], desc:"La enfermera del colegio tiene un feto pegado en la cara. El pueblo hace una semana de concientización.", why:"Sátira de la corrección política y las semanas de concientización que terminan siendo contraproducentes." },
  { id:129, title:"Summer Sucks", s:2, e:8, funny:7.9, dark:3, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo"], desc:"Los fuegos artificiales son ilegales. Un snake gigante destruye la ciudad. Mr. Garrison aprende a nadar.", why:"El snake gigante como catástrofe del 4 de julio es puro absurdismo de las primeras temporadas." },
  { id:130, title:"Cow Days", s:2, e:13, funny:8.2, dark:3, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","parodia"], desc:"South Park tiene su festival anual Cow Days. Cartman cree que es un cowboy vietnamita. Stan y Kyle apuestan.", why:"Cartman hipnotizado creyendo ser una prostituta vietnamita es uno de sus momentos más absurdos." },
  { id:131, title:"Clubhouses", s:2, e:12, funny:8.0, dark:4, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["personaje","absurdo"], desc:"Stan y Kyle construyen una casa del árbol. Sus padres se separan. Cartman construye la suya para hacer verdad o consecuencia.", why:"El paralelismo entre el drama familiar y la competencia de clubhouses funciona sorprendentemente bien." },

  // ── S3 extras ──
  { id:132, title:"Spontaneous Combustion", s:3, e:2, funny:8.1, dark:4, impact:6, auto:true, chars:["Randy","Stan","Kyle","Cartman","Kenny"], types:["absurdo","personaje"], desc:"La gente de South Park explota espontáneamente. Randy debe resolver el misterio científico.", why:"Randy como científico heroico es el precursor de los grandes arcos de Randy de las temporadas posteriores." },
  { id:133, title:"The Succubus", s:3, e:3, funny:8.2, dark:5, impact:6, auto:true, chars:["Chef","Stan","Kyle","Cartman","Kenny"], types:["absurdo","personaje"], desc:"Chef se enamora y va a casarse. Los chicos sospechan que su novia es una súcubo.", why:"Chef en modo romance es completamente diferente a lo habitual. El final es genuinamente oscuro." },
  { id:134, title:"Jackovasaurus", s:3, e:4, funny:7.6, dark:2, impact:5, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","parodia"], desc:"Los chicos encuentran una criatura estúpida e irritante que todo el mundo ama excepto Cartman.", why:"Parodia de la fiebre de los Jar Jar Binks. Diseñado deliberadamente para ser insoportable." },
  { id:135, title:"Cat Orgy", s:3, e:7, funny:8.3, dark:4, impact:7, auto:true, chars:["Cartman","Shelly"], types:["personaje","absurdo"], desc:"Cartman queda al cuidado de la hermana de Stan. Hay una orgía de gatos afuera. Shelly tiene novio rebelde.", why:"Cartman vs Shelly es una dinámica completamente distinta a la habitual. Cartman recibiendo lo que merece." },
  { id:136, title:"Two Guys Naked in a Hot Tub", s:3, e:8, funny:8.1, dark:3, impact:6, auto:true, chars:["Stan","Randy"], types:["absurdo","personaje"], desc:"Randy y otro padre se masturban juntos en el jacuzzi. Stan queda atrapado con los nerds en una fiesta de adultos.", why:"Precursor del arco de Randy como padre con inseguridades. El subplot de Stan con los nerds es adorable." },
  { id:137, title:"Starvin' Marvin in Space", s:3, e:13, funny:7.8, dark:3, impact:6, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","parodia"], desc:"Marvin regresa con una nave espacial. Los chicos lo ayudan a encontrar un planeta para su pueblo.", why:"Secuela que escala el absurdo al espacio exterior. La crítica a los misioneros es afilada." },

  // ── S4 extras ──
  { id:138, title:"The Tooth Fairy Tats 2000", s:4, e:1, funny:8.3, dark:5, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","personaje"], desc:"Cartman descubre cómo sacarle dinero al hada de los dientes. Hay un cartel de dientes de leche.", why:"Cartman construyendo una operación criminal desde el jardín de infantes es el Cartman en su forma más pura." },
  { id:139, title:"Quintuplets 2000", s:4, e:4, funny:7.9, dark:3, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","parodia"], desc:"Cinco niñas rumanas se quedan en South Park. Todo el pueblo quiere ser cantante de ópera.", why:"Parodia del caso Elián González mezclada con la fiebre de los reality de talento. Extraño y divertido." },
  { id:140, title:"Do the Handicapped Go to Hell?", s:4, e:9, funny:8.2, dark:6, impact:7, auto:true, chars:["Timmy","Cartman","Stan","Kyle","Kenny"], types:["personaje","absurdo"], desc:"Los chicos se preocupan por el alma de Timmy. Cartman funda su propia iglesia para recaudar dinero.", why:"Cartman como televangelista estafador es adelantado a su tiempo. Timmy como tema teológico es brillante." },
  { id:141, title:"Probably", s:4, e:10, funny:8.3, dark:6, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["personaje","político"], desc:"Cartman convierte su iglesia en un negocio millonario. Los chicos van al infierno. Saddam Hussein aparece.", why:"Continuación directa del anterior. La iglesia de Cartman como startup religiosa es brutalmente vigente." },
  { id:142, title:"Helen Keller! The Musical", s:4, e:13, funny:8.2, dark:3, impact:6, auto:true, chars:["Timmy","Stan","Kyle","Cartman","Kenny"], types:["parodia","personaje"], desc:"Los chicos hacen un musical de Helen Keller para el día de Thanksgiving. Timmy quiere que su pavo sea la estrella.", why:"Timmy y su pavo gobbler es una de las historias más tiernas de toda la serie." },

  // ── S5 extras ──
  { id:143, title:"It Hits the Fan", s:5, e:1, funny:8.5, dark:4, impact:8, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["meta","absurdo"], desc:"Una cadena de TV dice 'shit' al aire por primera vez. South Park la dice 162 veces. Una maldición antigua se activa.", why:"Episodio meta sobre la censura en TV. El contador de 'shit' en pantalla es una de las ideas más graciosas de la serie." },
  { id:144, title:"Cripple Fight", s:5, e:2, funny:8.6, dark:4, impact:7, auto:true, chars:["Timmy","Jimmy"], types:["personaje","absurdo"], desc:"Jimmy y Timmy pelean por ser el chico discapacitado popular del colegio. Big Gay Al es expulsado de los scouts.", why:"La pelea entre Jimmy y Timmy es una de las más largas y elaboradas de la historia del show." },
  { id:145, title:"The Entity", s:5, e:11, funny:8.4, dark:3, impact:7, auto:true, chars:["Kyle","Cartman"], types:["personaje","absurdo"], desc:"El primo de Kyle llega a South Park. Mr. Garrison inventa una nueva forma de transporte alternativo extremadamente perturbadora.", why:"El vehículo de Mr. Garrison es tan asqueroso que es gracioso. El primo del Kyle es un personaje único." },
  { id:146, title:"Here Comes the Neighborhood", s:5, e:12, funny:8.1, dark:6, impact:7, auto:true, chars:["Token","Stan","Kyle","Cartman","Kenny"], types:["político","absurdo"], desc:"Token quiere tener vecinos ricos. Atrae a celebridades negras ricas. El pueblo rural reacciona.", why:"Sátira racial sobre el clasismo disfrazado de racismo. Uno de los más inteligentes del período." },

  // ── S6 extras ──
  { id:147, title:"Jared Has Aides", s:6, e:1, funny:8.3, dark:4, impact:7, auto:true, chars:["Butters","Cartman"], types:["personaje","absurdo"], desc:"Butters suplanta a Cartman para hacer un comercial de una cadena de sándwiches. Jared de Subway tiene 'aides'.", why:"El juego de palabras central es brillante y sostenido durante todo el episodio." },
  { id:148, title:"Asspen", s:6, e:2, funny:8.4, dark:3, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["parodia","absurdo"], desc:"Las familias van a esquiar a Aspen. Stan debe competir en un duelo de esquí al estilo de los 80.", why:"Parodia perfecta de las películas de deportes de los 80. El antagonista es el arquetipo más exagerado posible." },
  { id:149, title:"Bebe's Boobs Destroy Society", s:6, e:10, funny:8.3, dark:4, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["absurdo","personaje"], desc:"Bebe empieza a desarrollarse y todos los chicos regresan a comportamientos primitivos.", why:"Sátira de cómo los hombres responden instintivamente a la biología. Gracioso y algo incómodo en el buen sentido." },
  { id:150, title:"Child Abduction is Not Funny", s:6, e:11, funny:8.2, dark:5, impact:7, auto:true, chars:["Tweek","Stan","Kyle","Cartman","Kenny"], types:["absurdo","político"], desc:"Los padres de South Park entran en pánico por los secuestradores. Construyen un muro y expulsan a los niños.", why:"Los padres aterrorizados por los medios construyendo un muro y expulsando a sus propios hijos es genial." },
  { id:151, title:"A Ladder to Heaven", s:6, e:12, funny:8.4, dark:6, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["dark","absurdo"], desc:"Los chicos construyen una escalera al cielo para encontrar el ticket de dulces de Kenny. Cartman bebe las cenizas de Kenny.", why:"Cartman bebiendo cenizas y empezando a recordar los recuerdos de Kenny es perturbadoramente gracioso." },

  // ── S7 extras ──
  { id:152, title:"Krazy Kripples", s:7, e:2, funny:8.4, dark:4, impact:7, auto:true, chars:["Timmy","Jimmy"], types:["personaje","absurdo"], desc:"Jimmy y Timmy forman un club solo para discapacitados de nacimiento. Christopher Reeve sorbe de los fetos.", why:"El uso de Christopher Reeve como villano chupando embriones es completamente de otro mundo." },
  { id:153, title:"Toilet Paper", s:7, e:3, funny:8.3, dark:4, impact:6, auto:true, chars:["Cartman","Kyle","Stan","Kenny"], types:["personaje","absurdo"], desc:"Los chicos empapelan la casa de su profesora de arte. Cartman manipula a Butters para que no confese.", why:"Cartman en modo manipulación psicológica sobre Butters. La intensidad del interrogatorio a Butters es brillante." },
  { id:154, title:"I'm a Little Bit Country", s:7, e:4, funny:8.3, dark:3, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["político","musical"], desc:"El pueblo se divide entre pro-guerra y anti-guerra en Iraq. Cartman viaja al pasado para entender a los Founding Fathers.", why:"El musical final que une a ambas facciones es absurdamente satisfactorio. La política como farsa." },
  { id:155, title:"South Park is Gay!", s:7, e:8, funny:8.5, dark:3, impact:8, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","absurdo"], desc:"Todo el pueblo se vuelve metrosexual. Kyle resiste. Los Queer Eye Guys resultan ser aliens Crab People.", why:"Parodia de la tendencia metrosexual del 2003 con el giro más absurdo posible." },
  { id:156, title:"Grey Dawn", s:7, e:10, funny:8.2, dark:5, impact:6, auto:true, chars:["Randy","Stan"], types:["absurdo","político"], desc:"Los ancianos de South Park conducen sin control destruyendo todo. Se rebelan y forman su propio estado.", why:"La rebelión de los ancianos como nación independiente es absurdamente gracioso." },
  { id:157, title:"Butt Out", s:7, e:13, funny:8.3, dark:4, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["político","absurdo"], desc:"Los chicos empiezan a fumar para no parecerse a los activistas anti-tabaco. Rob Reiner aparece como villano.", why:"Rob Reiner como villano gordo y manipulador es una de las sátiras de celebridades más salvajes." },

  // ── S8 extras ──
  { id:158, title:"Up the Down Steroid", s:8, e:2, funny:8.4, dark:5, impact:7, auto:true, chars:["Jimmy","Timmy","Cartman"], types:["personaje","absurdo"], desc:"Jimmy usa esteroides para ganar en los juegos especiales. Cartman finge ser discapacitado para competir.", why:"Jimmy con esteroides transformándose es completamente inesperado. Cartman en los juegos especiales es lo que esperarías." },
  { id:159, title:"The Passion of the Jew", s:8, e:3, funny:8.7, dark:6, impact:8, auto:true, chars:["Cartman","Kyle","Stan","Kenny"], types:["político","parodia"], desc:"Kyle ve La Pasión de Cristo y siente culpa. Cartman usa la película para liderar un movimiento antisemita.", why:"Sátira de La Pasión de Gibson y del antisemitismo que usa entretenimiento como pretexto." },
  { id:160, title:"You Got F'd in the A", s:8, e:4, funny:8.3, dark:4, impact:6, auto:true, chars:["Stan","Butters"], types:["parodia","absurdo"], desc:"Stan debe armar un equipo de baile para competir contra unos chicos de Orange County que los humillaron.", why:"Parodia de You Got Served. Butters tiene el mejor trauma secreto de toda la serie." },
  { id:161, title:"Awesom-O", s:8, e:5, funny:9.1, dark:3, impact:9, auto:true, chars:["Cartman","Butters"], types:["personaje","absurdo"], desc:"Cartman se disfraza de robot para espiar a Butters. Termina siendo usado por el ejército.", why:"Butters siendo adorable vs Cartman sufriendo las consecuencias. Uno de los mejores episodios de Butters." },
  { id:162, title:"The Jeffersons", s:8, e:6, funny:8.5, dark:6, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["político","personaje"], desc:"Un hombre adinerado se muda con su hijo. La policía lo acosa por ser negro y rico.", why:"Crítica al perfilamiento racial de la policía hacia personas negras adineradas. Oscuro y necesario." },
  { id:163, title:"Quest for Ratings", s:8, e:11, funny:8.3, dark:3, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Craig"], types:["parodia","meta"], desc:"Los chicos hacen un noticiero escolar. Craig tiene el programa más exitoso. Todos se drogan con medicinas para el resfriado.", why:"La competencia entre programas escolares parodia perfectamente la TV de ratings." },
  { id:164, title:"Stupid Spoiled Whore Video Playset", s:8, e:12, funny:8.6, dark:4, impact:8, auto:true, chars:["Wendy","Cartman"], types:["político","personaje"], desc:"Paris Hilton abre una tienda en South Park. Las nenas del colegio empiezan a imitar su estilo. Mr. Slave la derrota.", why:"La crítica a Paris Hilton y la hipersexualización de niñas es afilada y el final es completamente inesperado." },

  // ── S9 extras ──
  { id:165, title:"Mr. Garrison's Fancy New Vagina", s:9, e:1, funny:8.7, dark:6, impact:8, auto:true, chars:["Mr. Garrison","Kyle"], types:["político","absurdo"], desc:"Mr. Garrison se hace una operación de cambio de sexo. Kyle quiere operarse para poder jugar en la NBA.", why:"Uno de los primeros episodios sobre identidad de género en TV mainstream. Políticamente complejo incluso hoy." },
  { id:166, title:"Wing", s:9, e:3, funny:8.1, dark:3, impact:6, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","parodia"], desc:"Los chicos forman una agencia de talentos. Representan a Wing, una cantante china con voz muy peculiar.", why:"Wing era real — la cantante real participó. El contraste entre su voz y el contexto es absolutamente delirante." },
  { id:167, title:"Erection Day", s:9, e:7, funny:8.2, dark:4, impact:6, auto:true, chars:["Jimmy"], types:["personaje","absurdo"], desc:"Jimmy tiene erecciones incontrolables antes del show de talentos. Busca desesperadamente una solución.", why:"Jimmy como protagonista en un episodio completamente incómodo pero gracioso. El final es glorioso." },
  { id:168, title:"Two Days Before the Day After Tomorrow", s:9, e:8, funny:8.6, dark:4, impact:8, auto:true, chars:["Stan","Cartman","Randy"], types:["parodia","político"], desc:"Cartman y Stan rompen una represa por accidente. Todo el mundo culpa al calentamiento global al estilo The Day After Tomorrow.", why:"Parodia de la película catastrófica y del pánico climático. El 'I'm sorry' de Randy es un meme." },
  { id:169, title:"Bloody Mary", s:9, e:14, funny:8.4, dark:5, impact:7, auto:true, chars:["Randy","Stan"], types:["político","absurdo"], desc:"Randy es alcohólico. Una estatua de la Virgen sangra. Randy cree que es un milagro que lo cure.", why:"Sátira de las curas milagrosas y del tratamiento del alcoholismo como enfermedad inevitable." },

  // ── S10 extras ──

  { id:171, title:"Smug Alert!", s:10, e:2, funny:8.7, dark:4, impact:8, auto:true, chars:["Kyle","Stan","Randy"], types:["político","absurdo"], desc:"Gerald compra un auto híbrido y se vuelve insoportablemente smug. Una nube de smug destruye San Francisco.", why:"La nube de smug como fenómeno climático es la metáfora perfecta para la autocomplacencia liberal." },
  { id:172, title:"Tsst", s:10, e:7, funny:9.0, dark:5, impact:8, auto:true, chars:["Cartman","Mrs. Cartman"], types:["personaje","dark"], desc:"La mamá de Cartman llama al Dog Whisperer para controlar a Cartman. Cartman casi se convierte en buena persona.", why:"El único episodio donde Cartman genuinamente cambia… casi. Cesar Millan vs Cartman es perfecto." },
  { id:173, title:"Mystery of the Urinal Deuce", s:10, e:9, funny:8.5, dark:5, impact:7, auto:true, chars:["Cartman","Kyle","Stan"], types:["político","absurdo"], desc:"Alguien hizo caca en el urinario del colegio. Cartman cree que el 9/11 fue una conspiración del gobierno.", why:"Sátira brillante de las teorías conspirativas del 9/11 mezclada con el misterio más ridículo posible." },
  { id:174, title:"Hell on Earth 2006", s:10, e:11, funny:8.5, dark:5, impact:7, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","parodia"], desc:"Satán organiza una fiesta de Sweet Sixteen en el Infierno. Los tres asesinos más famosos deben conseguir una torta.", why:"Satán organizando una fiesta de 16 como Paris Hilton es uno de los mejores usos del personaje." },

  // ── S11 extras ──
  { id:175, title:"Cartman Sucks", s:11, e:2, funny:8.6, dark:5, impact:7, auto:true, chars:["Cartman","Butters"], types:["personaje","político"], desc:"Cartman toma fotos comprometedoras con Butters durmiendo. Butters es enviado a un campamento de conversión gay.", why:"Sátira de los campamentos de conversión gay. Butters siendo el más normal en el contexto más anormal." },
  { id:176, title:"Lice Capades", s:11, e:3, funny:8.2, dark:5, impact:6, auto:true, chars:["Cartman","Kyle","Stan","Kenny"], types:["absurdo","parodia"], desc:"Los chicos tienen piojos. Vista desde la perspectiva de los piojos, la cabeza de Cartman es su planeta.", why:"La parodia de Al Gore y el calentamiento global desde la perspectiva de los piojos es brillante." },
  { id:177, title:"The Snuke", s:11, e:4, funny:8.3, dark:6, impact:7, auto:true, chars:["Cartman","Kyle"], types:["político","parodia"], desc:"Cartman descubre una amenaza terrorista el día que Hillary Clinton llega a South Park. Parodia de 24.", why:"La parodia de 24 y del terrorismo post-9/11 está perfectamente ejecutada. Cartman como Jack Bauer es genial." },
  { id:178, title:"Fantastic Easter Special", s:11, e:5, funny:8.5, dark:5, impact:7, auto:true, chars:["Stan","Randy","Cartman","Kyle"], types:["absurdo","parodia"], desc:"Stan descubre que la Pascua esconde una conspiración de la Iglesia Católica con conejos guardianes del secreto.", why:"El Da Vinci Code pero con Pascua y conejos. Completamente ridículo y perfectamente ejecutado." },
  { id:179, title:"D-Yikes!", s:11, e:6, funny:8.3, dark:3, impact:6, auto:true, chars:["Mr. Garrison"], types:["personaje","absurdo"], desc:"Mr. Garrison descubre que es lesbiana. Los inmigrantes persas hacen el trabajo escolar de los chicos.", why:"El cambio de orientación de Garrison cada temporada llega a un punto totalmente absurdo aquí." },
  { id:180, title:"More Crap", s:11, e:9, funny:8.5, dark:3, impact:7, auto:true, chars:["Randy","Stan"], types:["absurdo","personaje"], desc:"Randy produce la cagada más grande de la historia. Bono resulta ser la cagada récord que nadie ha superado.", why:"El giro de que Bono es literalmente una cagada humana viviente es una de las ideas más ridículas y geniales." },
  { id:181, title:"Imaginationland Episode I", s:11, e:11, funny:8.8, dark:5, impact:8, auto:false, chars:["Cartman","Kyle","Butters"], types:["épico","absurdo"], desc:"Terroristas atacan Imaginationland. Los personajes imaginarios de toda la cultura pop cobran vida.", why:"El inicio de la trilogía más ambiciosa del show. Las referencias culturales son interminables." },
  { id:182, title:"Imaginationland Episode III", s:11, e:12, funny:8.7, dark:7, impact:8, auto:false, chars:["Cartman","Kyle","Butters"], types:["épico","dark"], desc:"La batalla final en Imaginationland. Butters debe imaginar a los buenos para derrotar a los malos.", why:"El cierre épico de la trilogía. Butters salvando el mundo con su imaginación es perfecto." },

  // ── S12 extras ──
  { id:183, title:"Canada on Strike", s:12, e:4, funny:8.5, dark:3, impact:8, auto:true, chars:["Cartman","Butters","Stan","Kyle","Kenny"], types:["político","absurdo"], desc:"Canadá hace huelga reclamando su parte de las ganancias de internet. Los chicos deben negociar.", why:"Los memes de 2008 como personajes físicos peleando entre sí es genuinamente hilarante." },
  { id:184, title:"Super Fun Time", s:12, e:7, funny:8.4, dark:5, impact:6, auto:true, chars:["Cartman","Butters","Stan","Kyle"], types:["personaje","absurdo"], desc:"Los chicos van de excursión a un museo pionero. Cartman arrastra a Butters a un parque de diversiones. Terroristas toman el museo.", why:"El giro de terroristas en el museo pionero contra los actores que deben mantenerse en personaje es genial." },
  { id:185, title:"The China Probrem", s:12, e:8, funny:8.6, dark:7, impact:8, auto:true, chars:["Cartman","Butters","Kyle"], types:["político","dark"], desc:"Cartman cree que China invadirá EE.UU. Los chicos intentan procesar el trauma de ver Indiana Jones 4.", why:"La película de Spielberg como trauma sexual es perturbadora y graciosísima. La China-fobia de Cartman es brillante." },
  { id:186, title:"Pandemic", s:12, e:10, funny:8.4, dark:4, impact:6, auto:false, chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["absurdo","parodia"], desc:"Los chicos son detenidos como los últimos panaméños en EE.UU. Randy filma todo como Cloverfield.", why:"Parodia de Cloverfield con cobayos gigantes. El subplot de Randy filmando todo es el mejor." },
  { id:187, title:"Elementary School Musical", s:12, e:13, funny:8.2, dark:2, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Butters"], types:["parodia","musical"], desc:"Todo el colegio está obsesionado con High School Musical. Stan debe unirse o perder a Wendy.", why:"Parodia de High School Musical con Butters completamente en su elemento como bailarín entusiasta." },

  // ── S13 extras ──
  { id:188, title:"Dances with Smurfs", s:13, e:13, funny:8.5, dark:4, impact:7, auto:true, chars:["Cartman","Wendy"], types:["político","parodia"], desc:"Cartman tiene un programa de radio matutino y ataca a Wendy como presidenta del consejo estudiantil.", why:"Parodia de los programas de radio AM y de la política estudiantil. Cartman como Glenn Beck es perfecto." },
  { id:189, title:"Eat, Pray, Queef", s:13, e:4, funny:8.2, dark:3, impact:6, auto:true, chars:["Cartman","Stan","Kyle","Kenny"], types:["absurdo","político"], desc:"Los queefs se vuelven el nuevo humor aceptable. Los hombres de South Park no lo soportan.", why:"La indignación de los chicos ante el humor de queef es el doble estándar del humor grosero perfectamente expuesto." },
  { id:190, title:"Butters' Bottom Bitch", s:13, e:9, funny:8.7, dark:5, impact:7, auto:true, chars:["Butters"], types:["personaje","absurdo"], desc:"Butters besa a una chica y la convierte en su prostituta. Construye accidentalmente un imperio de escort.", why:"Butters como proxeneta completamente inocente de lo que está haciendo es una de sus mejores historias." },
  { id:191, title:"W.T.F.", s:13, e:10, funny:8.4, dark:4, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","absurdo"], desc:"Los chicos se obsesionan con la lucha libre profesional. Forman su propia federación de wrestling.", why:"Los chicos haciendo promos de wrestling con total seriedad es uno de los mejores usos del formato parodia." },
  { id:192, title:"Pee", s:13, e:14, funny:8.3, dark:4, impact:6, auto:true, chars:["Cartman","Kyle","Stan","Kenny"], types:["absurdo","parodia"], desc:"El parque acuático está lleno de orina. Cartman va al parque con su gente. Parodia de 2012.", why:"La catástrofe apocalíptica del orina en el parque acuático y la parodia de 2012 funcionan perfectamente juntos." },

  // ── S14 extras ──
  { id:193, title:"Sexual Healing", s:14, e:1, funny:8.4, dark:5, impact:7, auto:true, chars:["Kyle","Stan","Cartman","Kenny"], types:["político","absurdo"], desc:"Los hombres famosos que tienen aventuras son diagnosticados con adicción al sexo. Kyle investiga la conspiración.", why:"La sátira de la adicción al sexo como excusa de famosos poderosos es perfectamente oportuna." },
  { id:194, title:"The Last of the Meheecans", s:15, e:9, funny:8.4, dark:4, impact:7, auto:true, chars:["Cartman","Butters","Kyle"], types:["político","absurdo"], desc:"Cartman lidera la patrulla fronteriza. Butters termina en México sin querer y se convierte en líder cultural.", why:"Butters accidentalmente liderando el movimiento de regreso de mexicanos a México es ridículo y brillante." },
  { id:195, title:"Ass Burgers", s:15, e:8, funny:8.3, dark:8, impact:7, auto:true, chars:["Stan","Cartman","Kyle"], types:["dark","personaje"], desc:"Stan sigue viendo todo como mierda después de sus 10 años. Descubre que el alcohol normaliza su visión.", why:"Continuación de You're Getting Old. El episodio más cercano a ser genuinamente oscuro sobre la depresión adulta." },

  // ── S16-17 extras ──
  { id:196, title:"Cartman Finds Love", s:16, e:7, funny:8.5, dark:4, impact:7, auto:true, chars:["Cartman","Kyle","Token"], types:["personaje","absurdo"], desc:"Una chica nueva llega al colegio. Cartman quiere que salga con Token porque ambos son negros. Cartman finge salir con Kyle.", why:"Cartman siendo racista de una manera completamente equivocada y retorcida. El giro de Kyle como 'novio' es oro." },
  { id:197, title:"Butterballs", s:16, e:5, funny:8.5, dark:6, impact:7, auto:true, chars:["Butters","Stan","Cartman"], types:["político","dark"], desc:"Butters es víctima de bullying. Stan hace un documental para explotarlo. Cartman hace una campaña de bullying.", why:"La doble sátira de los que abusan y los que explotan el bullying para fama propia es perfecta." },
  { id:198, title:"Going Native", s:16, e:11, funny:8.2, dark:4, impact:6, auto:true, chars:["Butters","Kenny"], types:["personaje","absurdo"], desc:"Butters se pone agresivo. Debe volver a Hawái para participar de un ritual nativo de nativos hawaianos blancos.", why:"El giro de que todos los de South Park son 'nativos hawaianos' es un absurdismo que funciona." },
  { id:199, title:"World War Zimmerman", s:17, e:3, funny:8.4, dark:6, impact:7, auto:true, chars:["Cartman","Token"], types:["político","dark"], desc:"Cartman tiene miedo de la reacción de Token ante el caso Trayvon Martin. Lo imagina como el paciente cero de un apocalipsis zombie.", why:"El miedo irracional de Cartman a la reacción negra como apocalipsis zombi es una sátira racial brillante." },
  { id:200, title:"Goth Kids 3: Dawn of the Posers", s:17, e:4, funny:8.3, dark:5, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny"], types:["parodia","absurdo"], desc:"Los góticos de South Park son convertidos en emos por una planta alienígena. Los góticos piden ayuda a los chicos.", why:"Los góticos como protagonistas serios en una crisis existencial es una premisa completamente absurda y bien ejecutada." },
  { id:201, title:"Taming Strange", s:17, e:5, funny:8.3, dark:4, impact:6, auto:true, chars:["Kyle","Ike"], types:["personaje","absurdo"], desc:"Ike pasa por una pubertad acelerada por un sistema de salud canadiense. Lorde lanza un nuevo álbum.", why:"Ike en pubertad acelerada como drama familiar es tierno y absurdo. El subplot de Randy-Lorde siempre funciona." },

  // ── S18-21 extras ──
  { id:202, title:"Cock Magic", s:18, e:8, funny:8.5, dark:4, impact:7, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["absurdo","parodia"], desc:"Los chicos descubren torneos clandestinos de gallos de pelea que en realidad son gallos haciendo magia.", why:"La ambigüedad deliberada del doble sentido sostenida durante todo el episodio es un logro de escritura." },
  { id:203, title:"#REHASH", s:18, e:10, funny:8.3, dark:4, impact:7, auto:false, chars:["Cartman","Kyle","Stan","Randy"], types:["político","meta"], desc:"Los chicos ya no hacen cosas, miran a otros hacerlos en streaming. Lorde lanza nueva música.", why:"La crítica al consumo pasivo de gaming en YouTube/Twitch antes de que fuera conversación mainstream." },
  { id:204, title:"Moss Piglet", s:21, e:8, funny:8.3, dark:4, impact:6, auto:true, chars:["Tweek","Craig","Cartman"], types:["personaje","absurdo"], desc:"Tweek y Craig crean un proyecto de ciencia sobre tardígrados. Cartman explota la relación para ganar.", why:"La relación Tweek-Craig siendo usada por Cartman como recurso es gracioso y tierno al mismo tiempo." },
  { id:205, title:"Hummels & Heroin", s:21, e:5, funny:8.4, dark:7, impact:7, auto:true, chars:["Stan","Randy"], types:["político","dark"], desc:"Los adultos mayores del hogar de ancianos están distribuyen heroína escondida en figuritas. Stan investiga.", why:"La epidemia de opioides contada desde una residencia de ancianos con figuritas es oscuramente brillante." },

  // ── S22-26 extras ──
  { id:206, title:"A Boy and a Priest", s:22, e:2, funny:8.3, dark:6, impact:6, auto:true, chars:["Butters","Stan","Kyle","Cartman","Kenny"], types:["político","absurdo"], desc:"Butters se hace amigo del padre Maxi. El Vaticano sospecha de la amistad y envía agentes.", why:"El Vaticano persiguiendo a Butters y al cura por una amistad inocente es la sátira de los escándalos de la Iglesia." },
  { id:207, title:"Time To Get Cereal", s:22, e:9, funny:8.6, dark:6, impact:7, auto:false, chars:["Cartman","Stan","Kyle","Kenny","Randy"], types:["dark","parodia"], desc:"ManBearPig resulta ser real. Al Gore tenía razón. Los chicos deben disculparse.", why:"La reversión del episodio original de ManBearPig donde todos deben reconocer que estaban equivocados es genial." },
  { id:208, title:"Nobody Got Cereal?", s:22, e:10, funny:8.5, dark:7, impact:7, auto:false, chars:["Cartman","Stan","Kyle","Kenny","Randy"], types:["dark","parodia"], desc:"ManBearPig continúa atacando. La sociedad hace un trato con él. Los chicos deben pagar el precio.", why:"El trato con ManBearPig como metáfora del cambio climático ignorado por conveniencia es oscuramente preciso." },
  { id:209, title:"Let Them Eat Goo", s:23, e:4, funny:8.3, dark:4, impact:6, auto:true, chars:["Cartman","PC Principal","Randy"], types:["político","absurdo"], desc:"PC Principal reemplaza la comida del colegio con opciones vegetales. Randy intenta salvar la industria cárnica.", why:"La batalla entre veganismo y la industria cárnica contada desde el comedor escolar." },
  { id:210, title:"Basic Cable", s:23, e:9, funny:8.2, dark:3, impact:6, auto:true, chars:["Kyle","Kenny","Cartman"], types:["absurdo","parodia"], desc:"Kenny no tiene Netflix ni streaming. Solo cable básico. Los chicos descubren lo que es el cable en 2019.", why:"El redescubrimiento del cable básico como rareza en la era del streaming es un chiste que no envejece." },
  { id:211, title:"Christmas Snow", s:23, e:10, funny:8.3, dark:3, impact:6, auto:true, chars:["Randy","Stan","Kyle","Cartman","Kenny"], types:["absurdo","musical"], desc:"El pueblo prohíbe el alcohol en Navidad. Randy intenta hacer nieve de marihuana para recuperar el espíritu navideño.", why:"Randy y la marihuana como solución a todos los problemas navideños es el arco de Tegridy Farms en su punto más absurdo." },
  { id:212, title:"The Scoots", s:22, e:5, funny:8.4, dark:4, impact:6, auto:true, chars:["Stan","Kyle","Cartman","Kenny","Randy"], types:["absurdo","político"], desc:"Los scooters eléctricos invaden South Park en Halloween. Los chicos no pueden salir a pedir dulces.", why:"Sátira de los e-scooters de Bird/Lime perfectamente oportuna en 2018." },
  { id:213, title:"Scott Malkinson in Control", s:23, e:7, funny:8.3, dark:4, impact:6, auto:true, chars:["Cartman","Scott Malkinson"], types:["personaje","absurdo"], desc:"Scott Malkinson es el nuevo presidente del consejo estudiantil. Cartman debe manipularlo desde atrás.", why:"Scott Malkinson como figura de poder accidental es una dinámica completamente nueva para el show." },
  { id:214, title:"Tegridy Farms Halloween Special", s:23, e:5, funny:8.2, dark:5, impact:6, auto:true, chars:["Randy","Stan"], types:["absurdo","dark"], desc:"Randy usa su marihuana para fabricar un producto especial de Halloween. Un fantasma asecha Tegridy Farms.", why:"Halloween en Tegridy Farms con el twist de que la marihuana tiene propiedades sobrenaturales." },
  { id:215, title:"Post Covid", s:25, e:5, funny:8.4, dark:6, impact:7, auto:false, chars:["Cartman","Stan","Kyle","Kenny"], types:["político","dark"], desc:"Special de Paramount+. 40 años en el futuro, los chicos están todos separados. Kenny murió del COVID.", why:"El salto al futuro con los personajes adultos es uno de los experimentos más audaces de las últimas temporadas." },
  { id:216, title:"Back To The Cold War", s:25, e:3, funny:8.4, dark:5, impact:6, auto:true, chars:["Randy","PC Principal"], types:["político","absurdo"], desc:"Randy teme que Rusia ataque Tegridy Farms. La nostalgia de la Guerra Fría invade el pueblo.", why:"Hecho con la invasión de Ucrania como telón de fondo. Nostalgias de la Guerra Fría como mecanismo de evasión." },
  { id:217, title:"Japanese Toilet", s:26, e:2, funny:8.4, dark:3, impact:6, auto:true, chars:["Randy","Stan"], types:["absurdo","parodia"], desc:"Randy queda obsesionado con los inodoros japoneses high-tech. Quiere uno para Tegridy Farms.", why:"La obsesión de Randy con tecnología doméstica japonesa es exactamente tan absurda como suena." },
  { id:218, title:"Spring Break", s:26, e:3, funny:8.3, dark:4, impact:6, auto:true, chars:["Randy","Stan"], types:["absurdo","parodia"], desc:"Los chicos van a Spring Break. Randy descubre que ya no es el público objetivo de nada.", why:"Randy enfrentando que ya no es joven es melancólico y gracioso al mismo tiempo." },
  { id:219, title:"Deep Learning", s:27, e:1, funny:8.6, dark:4, impact:7, auto:true, chars:["Stan","Cartman","Kyle","Kenny"], types:["político","parodia"], desc:"Stan usa IA para escribirle mensajes a Wendy. Cartman encuentra una forma de explotar ChatGPT en el colegio.", why:"La primera incursión profunda del show en la IA. La visión de Cartman sobre ChatGPT es perfectamente Cartman." },
  { id:220, title:"When Christmas Goes Wrong", s:27, e:2, funny:8.3, dark:4, impact:6, auto:true, chars:["Cartman","Butters","Kyle","Stan","Kenny"], types:["absurdo","personaje"], desc:"Los chicos arruinan un muñeco de nieve enorme del pueblo. Deben conseguir dinero para repararlo antes de Navidad.", why:"La dinámica de los chicos trabajando juntos para arreglar algo que Cartman arruinó es clásica y siempre funciona." },

  { id:222, title:"Not Suitable for Children", s:27, e:3, funny:8.4, dark:5, impact:7, auto:true, chars:["Randy","Stan","Cartman"], types:["político","absurdo"], desc:"OnlyFans queda disponible para menores. Randy y los padres de South Park entran en pánico total.", why:"La sátira de OnlyFans y la regulación del contenido adulto online es uno de los temas más vigentes de las últimas temporadas." },
];

const CHARS_LIST = ["Cartman","Stan","Kyle","Kenny","Butters","Randy","Jimmy","Wendy","Chef","Tweek","Craig","PC Principal"];

const CONTEXTS = {
  // ── S1 ──
  "Cartman Gets an Anal Probe": { aired:"13 de agosto de 1997", world:"Comedy Central era un canal menor. Nadie esperaba que un show de animación para adultos fuera a redefinir la TV.", controversy:"La cadena dudó en emitirlo por el lenguaje y las imágenes. El éxito de su estreno fue tan grande que renovaron inmediatamente.", legacy:"El episodio piloto que lanzó uno de los programas más influyentes de la historia de la televisión por cable." },
  "Weight Gain 4000": { aired:"20 de agosto de 1997", world:"El programa de Kathie Lee Gifford era uno de los más vistos de la mañana americana.", controversy:"Fue una de las primeras veces que SP atacó a una figura pública real con nombre y apellido.", legacy:"Estableció el modelo de sátira de celebridades que el show mantendría durante décadas." },
  "Big Gay Al's Big Gay Boat Ride": { aired:"3 de septiembre de 1997", world:"La representación gay positiva en TV era casi inexistente en 1997. Will & Grace aún no existía.", controversy:"Algunos canales afiliados se negaron a emitirlo. Ganó un GLAAD Award por representación positiva.", legacy:"Uno de los episodios más progresistas de la serie, adelantado a su época en materia de derechos LGBTQ+." },
  "Mr. Hankey the Christmas Poo": { aired:"17 de diciembre de 1997", world:"La guerra cultural de las fiestas en EE.UU. comenzaba a tomar forma. Los debates sobre la inclusión en Navidad eran nuevos.", controversy:"Mezclar Navidad con heces parlantes generó quejas masivas de grupos religiosos.", legacy:"Mr. Hankey se convirtió en un ícono tan reconocible que apareció en el desfile de Macy's. Un absurdo hecho realidad." },
  "Mecha-Streisand": { aired:"10 de septiembre de 1997", world:"Barbra Streisand era omnipresente en los medios, conocida por su ego y sus demandas de privacidad.", controversy:"Streisand nunca perdonó al show. Años después confirmó que la odiaba.", legacy:"El modelo para decenas de episodios con celebridades reales convertidas en monstruos o villanos." },
  "Cartman's Mom is a Dirty Slut": { aired:"25 de febrero de 1998", world:"Los cliffhangers de temporada eran la norma en la TV de los 90. Dallas, Twin Peaks habían definido el formato.", controversy:"El cliffhanger fue tan polémico que Comedy Central recibió miles de llamadas exigiendo la respuesta.", legacy:"Uno de los mejores cliffhangers de la historia de la TV animada." },

  // ── S2 ──
  "Cartman's Mom is Still a Dirty Slut": { aired:"22 de abril de 1998", world:"El país esperaba la respuesta al cliffhanger. Era la conversación en todas las oficinas.", controversy:"Trey y Matt tomaron el pelo a la audiencia durante meses. La respuesta final es completamente absurda.", legacy:"La revelación del padre de Cartman definió su lore para siempre." },
  "Gnomes": { aired:"16 de diciembre de 1998", world:"La fiebre de fusiones corporativas de los 90 estaba en su pico. Starbucks conquistaba el mundo.", controversy:"Fue interpretado como un ataque al movimiento anti-globalización y también al capitalismo. Ambas partes se sintieron atacadas.", legacy:"Los Underpants Gnomes y su plan de negocios son citados en clases de MBA hasta hoy." },
  "Chef's Salty Chocolate Balls": { aired:"19 de agosto de 1998", world:"Sundance y los festivales de cine indie vivían su época dorada con Pulp Fiction y Fargo como referentes.", controversy:"La canción de Chef superó las barreras del buen gusto pero fue un éxito comercial real.", legacy:"Demostró que SP podía hacer sátira cultural sofisticada mezclada con humor escatológico." },
  "Chickenpox": { aired:"26 de agosto de 1998", world:"El debate sobre la pobreza estructural en EE.UU. era parte del discurso político post-Clinton.", controversy:"Mostró la pobreza de Kenny con una dureza inusual para un show de animación.", legacy:"Uno de los primeros episodios en usar a Kenny para comentario social serio." },
  "City on the Edge of Forever": { aired:"20 de mayo de 1998", world:"Los clips shows eran un recurso habitual y detestado de la TV americana de los 90.", controversy:"Parodiar el propio formato del show al mostrar recuerdos incorrectos fue muy arriesgado para una serie joven.", legacy:"Un experimento meta que anticipó la autoconciencia que definiría al show en temporadas posteriores." },
  "Spookyfish": { aired:"28 de octubre de 1998", world:"Halloween se estaba convirtiendo en un negocio masivo en EE.UU., con especiales de TV de todo tipo.", controversy:"La parodia del universo espejo de Star Trek fue muy específica y muchos fans no captaron la referencia.", legacy:"El Cartman amable del universo espejo es uno de los conceptos más queridos del fandom." },

  // ── S3 ──
  "Sexual Harassment Panda": { aired:"7 de julio de 1999", world:"Los juicios por acoso sexual corporativos explotaban en EE.UU. post-Clinton/Lewinsky.", controversy:"Burlarse del acoso sexual con un panda fue considerado de muy mal gusto por grupos de mujeres.", legacy:"La metáfora del panda como herramienta corporativa es una de las más recordadas de las temporadas tempranas." },
  "Chinpokomon": { aired:"3 de noviembre de 1999", world:"La fiebre Pokémon estaba en su cúspide mundial. Las cartas valían fortunas y los niños peleaban por ellas.", controversy:"Japón protestó por la caricaturización de los japoneses con dientes pequeños y genitales enormes.", legacy:"Captura perfectamente la histeria colectiva del fenómeno Pokémon mejor que cualquier documental." },
  "Tweek vs. Craig": { aired:"23 de junio de 1999", world:"Los reality shows de peleas como Jerry Springer dominaban la TV americana.", controversy:"Fue relativamente inofensivo para los estándares del show, lo que lo hizo sobresalir por ser más character-driven.", legacy:"Estableció a Tweek y Craig como personajes propios que dos décadas después se convertirían en pareja oficial." },

  // ── S4 ──
  "Cartman Joins NAMBLA": { aired:"21 de junio de 2000", world:"El internet como herramienta para delincuentes sexuales era un tema nuevo y aterrador en los medios.", controversy:"Comedy Central recibió amenazas de demanda de NAMBLA real. El episodio fue uno de los más controvertidos hasta ese momento.", legacy:"Contiene uno de los mejores remates finales de la historia del show." },
  "Timmy 2000": { aired:"19 de abril de 2000", world:"El sobrediagnóstico de ADD/ADHD en niños era el tema del momento en pediatría y educación americana.", controversy:"Grupos de discapacitados protestaron aunque la sátira claramente apuntaba al sistema médico, no a Timmy.", legacy:"Introdujo a Timmy como uno de los personajes más queridos, demostrando que SP podía tratar la discapacidad con dignidad." },
  "Do the Handicapped Go to Hell?": { aired:"16 de agosto de 2000", world:"Los debates sobre fe y discapacidad eran recurrentes en la TV americana de televangelistas.", controversy:"Cartman como televangelista estafador fue considerado blasfemo por grupos religiosos.", legacy:"Prefiguró el Cartman manipulador de temporadas posteriores en su forma más elaborada." },
  "Kenny Dies": { aired:"5 de diciembre de 2001", world:"Los ataques del 11/9 habían transformado la TV americana. Los shows evitaban temas de muerte y trauma.", controversy:"Fue inesperadamente emotivo para un show conocido por matar a Kenny todas las semanas. Muchos fans lloraron.", legacy:"Demostró que South Park podía hacer drama genuino además de comedia. Un hito emocional de la serie." },

  // ── S5 ──
  "Scott Tenorman Must Die": { aired:"11 de julio de 2001", world:"Hannibal Lecter era el villano más icónico del cine en ese momento. El thriller psicológico dominaba las carteleras.", controversy:"El nivel de oscuridad del twist final dividió al fandom. Algunos dejaron de ver el show.", legacy:"Redefinió a Cartman como el villano más perturbador de la animación americana. Es considerado el mejor episodio de la serie." },
  "Towelie": { aired:"8 de agosto de 2001", world:"La guerra contra las drogas de Bush era el telón de fondo. 'Just Say No' era el mensaje oficial.", controversy:"Trey y Matt dijeron públicamente que era el peor personaje que habían creado. Fue un chiste meta que el fandom adoró.", legacy:"A pesar de ser descrito como 'el peor personaje', Towelie tiene merchandise, memes y apariciones décadas después." },
  "Cartmanland": { aired:"25 de julio de 2001", world:"Los parques temáticos eran el símbolo máximo del consumismo americano. Disney World era el paraíso capitalista.", controversy:"La crítica a Job y a Dios desde la perspectiva de Kyle fue considerada blasfema.", legacy:"Un estudio perfecto del egoísmo de Cartman y sus consecuencias inevitables. Frecuentemente citado como top 5 de la serie." },
  "Butters' Very Own Episode": { aired:"12 de diciembre de 2001", world:"Los escándalos de infidelidad política (Clinton, Condit) dominaban las noticias americanas.", controversy:"El final del episodio es uno de los más oscuros de toda la serie. Comedy Central lo consideró demasiado lejos.", legacy:"Estableció a Butters como personaje propio más allá de ser el reemplazo de Kenny, con su propia familia disfuncional." },
  "It Hits the Fan": { aired:"20 de junio de 2001", world:"La televisión americana debatía los límites del lenguaje. Cuando NBC dejó decir 'shit' en ER fue noticia nacional.", controversy:"Decir 'shit' 162 veces en pantalla fue un experimento deliberado de hasta dónde podían llegar.", legacy:"Uno de los comentarios más inteligentes sobre la censura televisiva en la historia de la TV americana." },
  "Cripple Fight": { aired:"27 de junio de 2001", world:"Los boy scouts americanos acababan de excluir a miembros gay, generando debate nacional.", controversy:"La pelea entre Jimmy y Timmy fue copiada exactamente de una pelea real de They Live (1988).", legacy:"El subplot de Big Gay Al y los scouts fue una de las primeras críticas directas al BSA años antes de que cambiaran su política." },
  "Super Best Friends": { aired:"4 de julio de 2001", world:"David Blaine estaba en su pico de fama con sus espectáculos de resistencia transmitidos en vivo por TV.", controversy:"Fue retirado de repetición después de los ataques del 11/9 por mostrar a Mohammed. Luego censurado permanentemente.", legacy:"Es de los episodios más difíciles de ver legalmente hoy, lo que le da un estatus mítico entre los fans." },

  // ── S6 ──
  "Professor Chaos": { aired:"10 de abril de 2002", world:"Reality shows como Survivor y American Idol redefinían la TV americana con sus formatos de eliminación.", controversy:"El formato de reality show para encontrar un nuevo amigo fue visto como una crítica directa y certera a estos programas.", legacy:"El origen de Professor Chaos es uno de los mejores episodios centrados en Butters de toda la serie." },
  "The Simpsons Already Did It": { aired:"26 de junio de 2002", world:"Los Simpsons llevaban 13 temporadas. Su sombra sobre la animación americana era total e inevitable.", controversy:"Fue una declaración de humildad y también de frustración creativa genuina de Trey y Matt.", legacy:"Un meta-episodio que discutió la originalidad en la era de la TV saturada antes de que fuera un tema mainstream." },
  "Red Hot Catholic Love": { aired:"3 de julio de 2002", world:"El escándalo de abuso sexual en la Iglesia Católica americana explotaba. El Boston Globe acababa de publicar su investigación histórica.", controversy:"Satirizar el abuso clerical mientras aún era noticia fresca fue considerado oportunista y valiente al mismo tiempo.", legacy:"Uno de los episodios más políticamente importantes del show, emitido exactamente cuando era más necesario." },
  "Return of the Fellowship": { aired:"30 de octubre de 2002", world:"El Señor de los Anillos: Las dos Torres acababa de estrenar. La fiebre tolkieniana era total.", controversy:"Mezclar LOTR con pornografía fue exactamente tan absurdo como suena pero funcionó perfectamente.", legacy:"La parodia más querida de Tolkien en formato corto. Referenciada constantemente en el fandom." },
  "A Ladder to Heaven": { aired:"6 de noviembre de 2002", world:"El primer aniversario del 11/9 había recargado el debate sobre la muerte y el más allá en America.", controversy:"Beber las cenizas de Kenny fue considerado de muy mal gusto incluso para los estándares del show.", legacy:"Expandió el universo de la muerte de Kenny de forma creativa y memorable." },
  "My Future Self n' Me": { aired:"4 de diciembre de 2002", world:"Las campañas anti-droga del gobierno americano usaban tácticas de miedo en escuelas.", controversy:"Exponer la hipocresía de los padres que contratan actores para asustar a sus hijos fue incómodo para muchos adultos.", legacy:"Uno de los mejores episodios sobre la hipocresía parental de las temporadas clásicas." },

  // ── S7 ──
  "Cancelled": { aired:"9 de abril de 2003", world:"Los reality shows de telerrealidad dominaban completamente la programación americana.", controversy:"La premisa de que la Tierra es un programa de TV fue interpretada como nihilismo por algunos críticos.", legacy:"Perfecto como secuela del piloto. Cierra el círculo con una meta-conciencia sofisticada." },
  "Fat Butt and Pancake Head": { aired:"16 de abril de 2003", world:"Jennifer Lopez estaba en su pico de fama con múltiples #1 y su relación con Ben Affleck en todos los medios.", controversy:"Jennifer Lopez amenazó con acciones legales que nunca llegaron. La parodia era demasiado absurda para prosperar.", legacy:"La dinámica de Cartman siendo su propia víctima sigue siendo una de las construcciones más ingeniosas del show." },
  "Lil' Crime Stoppers": { aired:"23 de abril de 2003", world:"Los policiales de acción como Bad Boys II y las películas de SWAT dominaban la taquilla.", controversy:"La violencia exagerada de los niños jugando a policías parodiaba el culto americano a las fuerzas del orden.", legacy:"La transición tonal del juego infantil al thriller adulto es uno de los cambios de registro más logrados de la serie." },
  "Christian Rock Hard": { aired:"29 de octubre de 2003", world:"El rock cristiano era una industria multimillonaria. Jars of Clay y Creed vendían millones.", controversy:"Las letras del disco de Cartman son exactamente canciones de amor con 'Jesus' reemplazando al amante.", legacy:"Cartman como ejecutivo musical sin escrúpulos prefigura la era de los artistas manufacturados." },
  "Casa Bonita": { aired:"12 de noviembre de 2003", world:"Casa Bonita era un restaurante real en Denver famoso entre los niños de Colorado.", controversy:"El episodio inmortalizó un restaurante local que luego se convirtió en destino de peregrinaje para fans de todo el mundo.", legacy:"Trey Parker compró Casa Bonita en 2021 para salvarlo de la quiebra post-COVID. La vida imitó al arte." },
  "All About Mormons": { aired:"19 de noviembre de 2003", world:"El musical The Book of Mormon no existía aún. Esta era la primera gran sátira del mormonismo en TV.", controversy:"La Iglesia SUD protestó pero el episodio fue elogiado por su precisión histórica y tono relativamente respetuoso.", legacy:"El episodio semilla de The Book of Mormon, el musical de Broadway que Trey y Matt crearían años después." },
  "Raisins": { aired:"10 de diciembre de 2003", world:"Hooters era símbolo del 'male gaze' americano. Breastaurants proliferaban en todo el país.", controversy:"La sexualización de una versión infantil de Hooters fue criticada con razón.", legacy:"El arco gótico de Stan y el corazón roto de Butters son de los momentos más emotivos del show." },

  // ── S8 ──
  "Good Times with Weapons": { aired:"17 de marzo de 2004", world:"El anime occidental vivía su boom con Cartoon Network y Toonami. Naruto y Dragon Ball Z eran fenómenos masivos.", controversy:"Butters siendo herido gravemente con una estrella ninja fue más oscuro de lo habitual.", legacy:"La animación estilo anime integrada es técnicamente impresionante y emocionalmente efectiva al mismo tiempo." },
  "AWESOM-O": { aired:"14 de abril de 2004", world:"Los reality shows de humillación como Jackass y Fear Factor dominaban la TV.", controversy:"El episodio es prácticamente un anime de Cartman siendo humillado repetidamente. Los fans lo adoraron.", legacy:"Butters en modo protagonista demostró que tenía potencial suficiente para su propio episodio centrado en él." },
  "Douche and Turd": { aired:"27 de octubre de 2004", world:"Las elecciones presidenciales Bush vs Kerry estaban en curso. Era la primera post-9/11 y la más polarizada en décadas.", controversy:"Presentar la elección presidencial como elegir entre una Douche y un Turd Sandwich ofendió a ambos partidos.", legacy:"La metáfora más repetida para describir el bipartidismo americano. Citada en artículos políticos serios hasta hoy." },
  "Goobacks": { aired:"28 de abril de 2004", world:"El debate sobre inmigración ilegal era el más caliente de la política americana ese año.", controversy:"La solución que propone el pueblo — algo que no podemos describir aquí — es una de las más perturbadoras de la serie.", legacy:"La parodia de la inmigración con viajeros del tiempo sigue siendo relevante en cada ciclo electoral." },
  "Woodland Critter Christmas": { aired:"15 de diciembre de 2004", world:"Los especiales de Navidad eran sagrados en la TV americana. Rudolph y Charlie Brown eran intocables.", controversy:"Subvertir el formato navideño con el giro más oscuro posible fue un shock total para la audiencia.", legacy:"Universalmente considerado el episodio más oscuro de toda la serie. Una obra maestra del subversión navideña." },
  "The Passion of the Jew": { aired:"31 de marzo de 2004", world:"La Pasión de Cristo de Mel Gibson acababa de estrenar y era la película más debatida del año.", controversy:"Acusar a Gibson de usar su película para antisemitismo fue muy polémico justo en el pico de su popularidad.", legacy:"Dos años después Gibson fue arrestado por conducir ebrio y hacer comentarios antisemitas. El show tenía razón." },
  "Stupid Spoiled Whore Video Playset": { aired:"1 de diciembre de 2004", world:"Paris Hilton era la celebridad más omnipresente de los medios. El sex tape de 2003 la había catapultado.", controversy:"La crítica a la hipersexualización de niñas usando a Paris Hilton como símbolo fue muy directa.", legacy:"Mr. Slave derrotando a Paris Hilton es uno de los finales más perturbadores y satisfactorios del show." },
  "Up the Down Steroid": { aired:"24 de marzo de 2004", world:"El escándalo de esteroides en la MLB (Barry Bonds, etc.) dominaba las noticias deportivas americanas.", controversy:"Jimmy usando esteroides y volviéndose violento con su novia fue uno de los momentos más incómodos de la S8.", legacy:"Jimmy como protagonista dramático demostró que SP podía hacer character study serio con personajes secundarios." },

  // ── S9 ──
  "Mr. Garrison's Fancy New Vagina": { aired:"9 de marzo de 2005", world:"Los debates sobre cirugías de reasignación de sexo comenzaban a llegar al mainstream americano.", controversy:"Fue uno de los primeros tratamientos del tema transgénero en TV de alcance masivo. Muy polémico por su enfoque.", legacy:"Iniciador de décadas de episodios de SP sobre identidad de género, siempre desde ángulos controversiales." },
  "Die Hippie Die": { aired:"16 de marzo de 2005", world:"Los festivales de música como Coachella y Bonnaroo comenzaban su era moderna. La cultura hippie revivía.", controversy:"Cartman como exterminador de hippies fue acusado de promover la intolerancia hacia contracultura.", legacy:"Slayer salvando South Park de los hippies es un momento que vive en el imaginario colectivo del metal." },
  "Best Friends Forever": { aired:"30 de marzo de 2005", world:"El caso Terri Schiavo dividía a America. El debate sobre el derecho a morir estaba en todas partes.", controversy:"Parodiar el caso Schiavo mientras la familia vivía la tragedia fue considerado de una crueldad innecesaria.", legacy:"Ganó el Emmy a Mejor Programa Animado en 2005. El timing fue impecable." },
  "The Losing Edge": { aired:"20 de abril de 2005", world:"El béisbol infantil americano era una institución. Cada padre quería que su hijo fuera el próximo A-Rod.", controversy:"Subvertir la narrativa del deporte infantil mostrando que los niños odian jugarlo fue refrescantemente honesto.", legacy:"Randy borracho peleándose en el béisbol es uno de los momentos más citados del personaje en toda la serie." },
  "The Death of Eric Cartman": { aired:"27 de abril de 2005", world:"Los Ghost Whisperer y Medium dominaban la TV. La moda de los médiums y contactar con muertos estaba en su pico.", controversy:"Ver a Cartman genuinamente asustado y vulnerable fue un quiebre de personaje que algunos fans no aceptaron.", legacy:"La dinámica Cartman-Butters en este contexto es de las más ricas de la serie." },
  "Ginger Kids": { aired:"9 de noviembre de 2005", world:"El bullying escolar por apariencia física era tema de debate en educación americana.", controversy:"Aunque la sátira era anti-discriminación, fue acusado de fomentar el gingerism. Hubo casos de bullying a pelirrojos después.", legacy:"El término 'gingers have no soul' se convirtió en meme global que aún circula 20 años después." },
  "Trapped in the Closet": { aired:"16 de noviembre de 2005", world:"La Cienciología estaba en su pico de popularidad mediática gracias a Tom Cruise y el estreno de War of the Worlds.", controversy:"Tom Cruise y John Travolta amenazaron con demandar. Isaac Hayes (Chef) renunció al show por su fe Cienciológica.", legacy:"Fue retirado de su repetición programada. Considerado uno de los episodios más valientes de la TV americana." },
  "Free Willzyx": { aired:"30 de noviembre de 2005", world:"Free Willy era la película de orcas más famosa. El debate sobre el cautiverio de orcas ya existía.", controversy:"El final del episodio es brutalmente realista sobre lo que le pasa a la orca. Los fans quedaron con el corazón roto.", legacy:"Uno de los finales más inesperados y oscuros de una premisa que comenzó siendo completamente tonta." },
  "Marjorine": { aired:"26 de octubre de 2005", world:"Desperate Housewives y los dramas de suburbio eran el género televisivo más popular del momento.", controversy:"Los padres de Butters creyéndolo muerto y enterrándolo vivo fue uno de los momentos más perturbadores del show.", legacy:"Butters disfrazado de niña es uno de los disfraces más icónicos del personaje y del show." },
  "Two Days Before the Day After Tomorrow": { aired:"19 de octubre de 2005", world:"El huracán Katrina había azotado Nueva Orleans semanas antes. La respuesta del gobierno fue catastrófica.", controversy:"Satirizar la negación del gobierno y la ciudadanía ante el cambio climático mientras Katrina era noticia fue arriesgado.", legacy:"El 'I'm sorry' de Stan como solución a todo es uno de los mejores gags recurrentes de Randy." },

  // ── S10 ──
  "The Return of Chef": { aired:"22 de marzo de 2006", world:"Isaac Hayes había renunciado al show citando su fe Cienciológica tras 'Trapped in the Closet'.", controversy:"Usar el audio de Hayes de episodios anteriores para 'matar' al personaje fue brutal pero legalmente válido.", legacy:"Uno de los momentos más dolorosos del show. La despedida de un personaje amado por circunstancias reales." },
  "Cartoon Wars": { aired:"5-12 de abril de 2006", world:"La crisis de las caricaturas de Mahoma en Dinamarca había generado violencia internacional meses antes.", controversy:"Comedy Central censuró el segmento que mostraba a Mahoma. Trey y Matt protestaron públicamente.", legacy:"Una de las pocas veces que Comedy Central censuró al show. El debate sobre autocensura sigue vigente." },
  "ManBearPig": { aired:"26 de abril de 2006", world:"Una Verdad Incómoda de Al Gore acababa de estrenar. El debate climático llegaba al mainstream.", controversy:"Burlar el alarmismo climático de Gore en 2006 fue criticado como negacionismo. El show revisó su postura en S22.", legacy:"ManBearPig volvió en S22 como real. Trey y Matt reconocieron que estaban equivocados. Una de las pocas autocríticas del show." },
  "Make Love, Not Warcraft": { aired:"4 de octubre de 2006", world:"World of Warcraft tenía 8 millones de suscriptores. Era el fenómeno cultural gamer más grande de la historia.", controversy:"Blizzard colaboró activamente con el episodio, prestando activos del juego. Un hito en la relación entre TV e industria gamer.", legacy:"Ganó el Emmy en 2007. Considerado el mejor episodio de la historia del show por muchos fans." },
  "Tsst": { aired:"7 de junio de 2006", world:"El Dog Whisperer de Cesar Millan era uno de los programas de cable más vistos en America.", controversy:"Ver a Cartman casi reformarse fue desconcertante para fans que preferían al Cartman puro maldad.", legacy:"El único episodio donde Cartman genuinamente cambia, aunque sea brevemente. Un estudio psicológico fascinante." },
  "Smug Alert!": { aired:"29 de marzo de 2006", world:"El Toyota Prius era el símbolo del consumidor consciente americano. La autosatisfacción ambiental era un fenómeno cultural.", controversy:"Criticar a los compradores de autos híbridos por su autosatisfacción fue impopular en los círculos progresistas.", legacy:"La nube de smug como metáfora climática es más relevante cada año con el crecimiento de las redes sociales." },
  "Mystery of the Urinal Deuce": { aired:"11 de octubre de 2006", world:"Las teorías conspirativas del 9/11 proliferaban en internet. 9/11 Truth era un movimiento con millones de seguidores.", controversy:"Satirizar las teorías conspirativas del 9/11 fue criticado por reducir preguntas legítimas a absurdo.", legacy:"Uno de los comentarios más inteligentes sobre la psicología de las teorías conspirativas antes de que fueran mainstream." },
  "Go God Go": { aired:"1-8 de noviembre de 2006", world:"La Wii de Nintendo se lanzaba ese mismo mes. Las colas para conseguirla eran de días.", controversy:"La crítica al dogmatismo ateo en el mismo nivel que el religioso molestó a ambos bandos.", legacy:"Richard Dawkins aparece en persona. Su reacción al episodio fue curiosamente positiva." },

  // ── S11 ──
  "With Apologies to Jesse Jackson": { aired:"7 de marzo de 2007", world:"Los debates sobre el lenguaje políticamente correcto y el uso de slurs raciales en medios eran intensos.", controversy:"Usar la n-word sin censura en TV fue extremadamente controversial aunque la intención era crítica.", legacy:"Uno de los mejores episodios sobre la dinámica racial en América. Muy citado en clases de estudios culturales." },
  "Le Petit Tourette": { aired:"3 de octubre de 2007", world:"El síndrome de Tourette era poco conocido por el público general y frecuentemente mal entendido.", controversy:"Fingir el Tourette para insultar impunemente capturó una fantasía antisocial universal de manera brillante.", legacy:"El plan que le explota en la cara a Cartman de la manera más satisfactoria posible. Un episodio perfecto." },
  "Imaginationland": { aired:"17 de octubre - 14 de noviembre de 2007", world:"El cine fantástico vivía su era dorada post-LOTR y Narnia. Los mundos imaginarios eran el género más taquillero.", controversy:"La saga de que Kyle debía 'succionar' a Cartman fue demasiado para algunos afiliados de Comedy Central.", legacy:"Ganó el Emmy en 2008. La trilogía más ambiciosa del show y una de las mejor construidas." },
  "Guitar Queer-O": { aired:"7 de noviembre de 2007", world:"Guitar Hero III acababa de salir y era el juego más vendido del año. La cultura del músico de plástico estaba en su pico.", controversy:"Describir Guitar Hero como adictivo y destructivo de relaciones fue presciente de los debates sobre adicción a videojuegos.", legacy:"Parodia perfecta de los biopics de rockstars décadas antes de que Bohemian Rhapsody los pusiera de moda de nuevo." },
  "The List": { aired:"14 de noviembre de 2007", world:"Las redes sociales nacientes (Facebook tenía 2 años) comenzaban a cuantificar la popularidad social.", legacy:"Anticipó perfectamente el mundo de los rankings sociales digitales que definirían la próxima década." },

  // ── S12 ──
  "Britney's New Look": { aired:"26 de marzo de 2008", world:"Britney Spears vivía su colapso público más extremo: raparse la cabeza, las fotos sin ropa interior, la pérdida de sus hijos.", controversy:"Satirizar la explotación mediática de su colapso mientras ocurría fue considerado parte del problema.", legacy:"Proféticamente, la industria continuó explotando a Britney durante 13 años más. SP lo vio venir." },
  "Major Boobage": { aired:"26 de marzo de 2008", world:"La tendencia de drogarse con cosas cotidianas (jengibre, pegamento) era noticia recurrente en medios americanos.", controversy:"La parodia de Heavy Metal fue tan fiel que los creadores originales la elogiaron.", legacy:"El episodio más visualmente ambicioso de la serie hasta ese momento." },
  "Over Logging": { aired:"16 de abril de 2008", world:"El acceso a internet pasaba de ser privilegio a necesidad básica. La dependencia digital comenzaba a ser obvia.", controversy:"El Randy masturbándose frente a internet nuevo fue demasiado explícito para algunos afiliados.", legacy:"La sátira de la adicción a internet se volvió más relevante con cada año que pasó." },
  "Breast Cancer Show Ever": { aired:"15 de octubre de 2008", world:"Las campañas de concientización sobre el cáncer de mama eran ubicuas. Todos usaban cintitas rosas.", controversy:"Usar el cáncer de mama como pretexto para una pelea de recreo fue de muy mal gusto según grupos de salud.", legacy:"La satisfacción catártica de ver a Cartman recibir lo que merece es uno de los mejores payoffs del show." },
  "About Last Night...": { aired:"5 de noviembre de 2008", world:"Barack Obama acababa de ganar las elecciones presidenciales. Era la madrugada más histórica en décadas.", controversy:"El episodio fue escrito y producido EN LA NOCHE de la elección. Se emitió 24 horas después de conocerse el resultado.", legacy:"El récord de producción más rápido del show. Una hazaña técnica además de creativa." },
  "Tonsil Trouble": { aired:"2 de abril de 2008", world:"El cocktail antirretroviral había convertido el VIH en una enfermedad crónica manejable, no una condena de muerte.", controversy:"Banalizar el VIH fue criticado por organizaciones de lucha contra el SIDA.", legacy:"Magic Johnson como portador accidental de la cura fue un giro absurdo que funcionó perfectamente." },

  // ── S13 ──
  "Margaritaville": { aired:"25 de marzo de 2009", world:"La crisis financiera de 2008 había destruido la economía global. El rescate bancario de Bush y Obama era noticia diaria.", controversy:"Satirizar el consumismo como causa de la crisis mientras los bancos recibían rescates fue extremadamente preciso.", legacy:"Uno de los comentarios económicos más inteligentes en la historia de la TV americana. Kyle como Jesús económico es perfecto." },
  "Fishsticks": { aired:"8 de abril de 2009", world:"Kanye West acababa de interrumpir el VMAs de Taylor Swift. Era el personaje más odiado del pop.", controversy:"Kanye West reaccionó al episodio en su blog diciendo que lo había hecho reflexionar. Luego lo desmintió.", legacy:"El chiste de los fishsticks circula en internet 15 años después. Uno de los mejores episodios de Cartman." },
  "The Ring": { aired:"11 de marzo de 2009", world:"Los Jonas Brothers eran el grupo teen más popular del mundo. Sus anillos de castidad eran tema de debate.", controversy:"Criticar a Disney por hipersexualizar a adolescentes usando la castidad como marketing fue brillante y correcto.", legacy:"La crítica al modelo de negocio de Disney con artistas adolescentes anticipó escándalos que vendrían años después." },
  "The Coon": { aired:"18 de marzo de 2009", world:"The Dark Knight había reinventado el cine de superhéroes. Todos querían ser vigilantes nocturnos.", controversy:"El nombre The Coon generó controversia por ser un slur racial en inglés. Fue intencional para generar incomodidad.", legacy:"Inicio del arco de superhéroes de Cartman que se expandió en S14 con una trilogía completa." },
  "Whale Whores": { aired:"28 de octubre de 2009", world:"Whale Wars de Animal Planet era el reality show más polémico. Sea Shepherd era amado y odiado.", controversy:"La revelación histórica final del episodio es una de las más absurdas y ofensivas del show.", legacy:"Randy Marsh formando una banda de death metal es el mejor subplot que no esperabas necesitar en tu vida." },
  "Butters' Bottom Bitch": { aired:"14 de octubre de 2009", world:"El debate sobre la legalización de la prostitución comenzaba en varios estados americanos.", controversy:"Butters construyendo un imperio de proxeneta sin entender qué hacía fue criticado por normalizar la explotación.", legacy:"Butters en modo empresario inocente es uno de los mejores usos del personaje. El cop subplot es glorioso." },

  // ── S14 ──
  "The Tale of Scrotie McBoogerballs": { aired:"24 de marzo de 2010", world:"El fenómeno de buscar significados ocultos en obras de arte y literatura estaba en su apogeo académico.", controversy:"El libro más asqueroso del mundo que se convierte en bestseller es la metáfora perfecta de la crítica literaria snob.", legacy:"Una de las críticas más inteligentes al mundo literario y a la proyección de significado en el arte." },
  "Medicinal Fried Chicken": { aired:"31 de marzo de 2010", world:"Colorado y otros estados comenzaban a legalizar la marihuana medicinal. KFC era omnipresente en América.", controversy:"Randy usando cáncer de testículos para conseguir marihuana fue clínicamente perturbador y gracioso.", legacy:"Cartman como Scarface del KFC sigue siendo uno de los mejores subplots paralelos de la serie." },
  "You Have 0 Friends": { aired:"7 de abril de 2010", world:"Facebook tenía 400 millones de usuarios. La red social había transformado las relaciones personales.", controversy:"Kyle atrapado dentro de Facebook como videojuego Tron fue demasiado absurdo para algunos pero perfecto para otros.", legacy:"La sátira de la adicción a Facebook anticipó el debate sobre redes sociales y salud mental por una década." },
  "200": { aired:"14 de abril de 2010", world:"Era el episodio número 200 del show. Hacía 13 años desde el piloto.", controversy:"La censura de Mohammed en el episodio 200 y 201 fue el mayor escándalo de censura en la historia del show.", legacy:"El episodio meta definitivo. Reúne a todos los enemigos del show en un homenaje a su propia historia." },
  "HumancentiPad": { aired:"27 de abril de 2011", world:"El iPad acababa de salir. Apple era la empresa más valiosa del mundo. Nadie leía los términos y condiciones.", controversy:"La premisa del Human Centipede + iTunes fue tan extrema que algunos canales no lo emitieron.", legacy:"La metáfora de no leer los términos y condiciones se convirtió en referencia estándar en debates sobre privacidad digital." },
  "Crack Baby Athletic Association": { aired:"11 de mayo de 2011", world:"El escándalo de la NCAA explotaba. Los atletas universitarios generaban millones sin recibir salario.", controversy:"Usar bebés adictos al crack para satirizar la explotación deportiva universitaria fue considerado demasiado oscuro.", legacy:"La sátira más directa y precisa de la explotación económica del deporte universitario americano." },
  "You're Getting Old": { aired:"8 de junio de 2011", world:"Trey Parker y Matt Stone acababan de estrenar The Book of Mormon en Broadway con éxito masivo.", controversy:"El episodio fue interpretado como una declaración de que el show terminaría pronto. Generó pánico en los fans.", legacy:"El episodio más honesto emocionalmente sobre la edad y el cinismo. Un shock total para la audiencia." },

  // ── S15 ──
  "Broadway Bro Down": { aired:"5 de octubre de 2011", world:"The Book of Mormon de Parker y Stone arrasaba en Broadway. Los musicales estaban más de moda que nunca.", controversy:"La teoría de que los musicales son básicamente publicidades de sexo oral fue absurda pero imposible de olvidar.", legacy:"Meta-comentario de Parker y Stone sobre su propia obra de Broadway. Una broma interna glorificada." },
  "1%": { aired:"19 de octubre de 2011", world:"El movimiento Occupy Wall Street ocupaba Zuccotti Park en Nueva York. El 1% vs el 99% era el debate central.", controversy:"Cartman siendo el 1% del colegio fue una apropiación cómica del lenguaje político que molestó a algunos activistas.", legacy:"Captura perfectamente la energía y las contradicciones del movimiento Occupy en su pico de visibilidad." },

  // ── S16 ──
  "Cash For Gold": { aired:"14 de marzo de 2012", world:"Los canales de teletienda de joyería eran un negocio multimillonario que explotaba a adultos mayores solitarios.", controversy:"Mostrar el ciclo de explotación con una dureza casi documental fue más oscuro que el humor habitual del show.", legacy:"Una de las críticas sociales más efectivas y menos cómicas del show. Genuinamente oscura." },
  "Sarcastaball": { aired:"26 de septiembre de 2012", world:"La NFL debatía el protocolo de concusiones. Junior Seau se había suicidado meses antes.", controversy:"Satirizar el debate sobre la seguridad en el fútbol americano mientras era una crisis real de salud fue muy oportuno.", legacy:"Randy destruyendo el deporte más americano por sarcasmo accidental es un concepto brillante." },
  "Raising the Bar": { aired:"3 de octubre de 2012", world:"El término 'lowering the bar' era omnipresente en debates culturales. Honey Boo Boo era el símbolo del reality trash.", controversy:"Atacar a un niño obeso en un scooter de movilidad fue uno de los momentos más incómodos del show.", legacy:"James Cameron bajando el bar en el fondo del océano es una de las imágenes más absurdas del show." },
  "A Nightmare on Face Time": { aired:"24 de octubre de 2012", world:"Blockbuster Video cerraba sus últimas tiendas. La era del streaming remplazaba al VHS y DVD.", controversy:"Usar la muerte de Blockbuster como escenario de terror fue dolorosamente preciso para los nostálgicos.", legacy:"El homenaje definitivo al Blockbuster muriente. Stan y Kyle en FaceTime anticipó el Halloween pandémico de 2020." },

  // ── S17 ──
  "Informative Murder Porn": { aired:"25 de septiembre de 2013", world:"True Crime y los documentales de crímenes reales comenzaban su era dorada en Netflix y cable.", controversy:"Los hijos bloqueando a sus padres de programas violentos fue la inversión perfecta del discurso tradicional.", legacy:"Anticipó el fenómeno Making a Murderer y la obsesión cultural con true crime por dos años." },
  "Black Friday": { aired:"13-27 de noviembre de 2013", world:"Game of Thrones estaba en su pico cultural post-Boda Roja. Black Friday se volvía cada vez más violento.", controversy:"La trilogía fue el proyecto más ambicioso del show hasta ese momento, criticado por algunos como 'demasiado para la TV'.", legacy:"La parodia más elaborada de Game of Thrones en cualquier medio. Referenciada en la propia comunidad GoT." },
  "World War Zimmerman": { aired:"2 de octubre de 2013", world:"El veredicto de no culpabilidad de George Zimmerman había generado el movimiento Black Lives Matter.", controversy:"El miedo de Cartman al apocalipsis negro fue una sátira del racismo sistémico muy directa y muy controvertida.", legacy:"Uno de los episodios más políticamente valientes sobre raza que el show había producido hasta entonces." },

  // ── S18 ──
  "The Cissy": { aired:"1 de octubre de 2014", world:"El debate sobre identidad de género en escuelas era uno de los más calientes de la política americana.", controversy:"Randy siendo Lorde fue completamente absurdo pero la canción era real y el sello discográfico lo aprobó.", legacy:"Cartman fingiendo ser trans para acceder al baño femenino anticipó exactamente el debate político de los años siguientes." },
  "Freemium Isn't Free": { aired:"5 de noviembre de 2014", world:"Clash of Clans y Candy Crush generaban miles de millones con microtransacciones. La adicción a juegos móviles era nueva.", controversy:"Describir los juegos freemium como diseñados por el Diablo para explotar la adicción fue una crítica radical y correcta.", legacy:"Uno de los análisis más precisos del modelo de negocio freemium en cualquier medio de comunicación." },
  "Grounded Vindaloop": { aired:"5 de noviembre de 2014", world:"La realidad virtual con Oculus (recién adquirido por Facebook) era el tema del momento en tecnología.", controversy:"Las capas de meta-realidad llegando a customer service real fue una de las ideas más originales del show.", legacy:"Considerado uno de los episodios más inventivos de las últimas temporadas. La construcción de capas es impecable." },

  // ── S19 ──
  "Stunning and Brave": { aired:"16 de septiembre de 2015", world:"Caitlyn Jenner había aparecido en Vanity Fair. Los debates sobre identidad de género dominaban los medios.", controversy:"PC Principal fue interpretado como un ataque al movimiento progresista. También como una crítica al backlash conservador.", legacy:"PC Principal se convirtió en uno de los personajes más ricos de las temporadas recientes." },
  "You're Not Yelping": { aired:"7 de octubre de 2015", world:"Yelp era la aplicación de reviews más usada. Los críticos amateur con poder de destruir negocios eran un fenómeno nuevo.", controversy:"La canción de los Yelpers sobre su poder destructivo fue alabada por restauradores reales como devastadoramente precisa.", legacy:"La sátira de la cultura de reviews online sigue siendo perfectamente vigente en la era de Google Reviews." },
  "Tweek x Craig": { aired:"28 de octubre de 2015", world:"El yaoi (romance masculino en anime) era un género masivo online. Las comunidades de fanfiction eran enormes.", controversy:"El tratamiento de la identidad LGBTQ+ en personajes menores fue elogiado por muchos como positivo e innovador.", legacy:"Tweek y Craig se convirtieron en pareja oficial del show. Sus figuras son las más vendidas del merchandise." },
  "Sponsored Content": { aired:"18 de noviembre de 2015", world:"El contenido patrocinado no etiquetado invadía medios. BuzzFeed era el símbolo del periodismo corrompido por publicidad.", controversy:"La crítica al periodismo nativo fue tan precisa que medios de comunicación reales se sintieron aludidos.", legacy:"Jimmy como último periodista honesto es una de las mejores caracterizaciones de la serie. Proféticamente vigente." },

  // ── S20 ──
  "Member Berries": { aired:"14 de septiembre de 2016", world:"Las elecciones Trump vs Clinton dividían América. La nostalgia de los 80/90 era la industria cultural dominante.", controversy:"Las Member Berries como metáfora de la nostalgia tóxica fueron incomprendidas por los nostálgicos que las adoptaron.", legacy:"La metáfora cultural más precisa del show sobre el MAGA y la nostalgia como herramienta política." },

  // ── S21 ──
  "White People Renovating Houses": { aired:"13 de septiembre de 2017", world:"Los asistentes de voz (Alexa, Google Home) irrumpían en los hogares. Los Confederados del Sur protestaban en Charlottesville.", controversy:"Conectar los Confederados con el miedo al desempleo por automatización fue una interpretación original y polémica.", legacy:"Una de las mejores sátiras de la era Trump sobre el resentimiento económico y cultural." },
  "Put It Down": { aired:"20 de septiembre de 2017", world:"Trump twitteaba sobre Corea del Norte regularmente, amenazando con acción militar. La tensión nuclear era real.", controversy:"Tratar la ansiedad nuclear adolescente con ternura fue un cambio de tono inesperado y muy efectivo.", legacy:"El mejor episodio centrado en la relación Tweek-Craig después de su episodio de origen." },
  "Franchise Prequel": { aired:"4 de octubre de 2017", world:"El universo de superhéroes Marvel dominaba la cultura pop. Facebook era investigado por su rol en las elecciones de 2016.", controversy:"Zuckerberg como villano meses antes de su comparecencia en el Congreso fue sorprendentemente profético.", legacy:"El uso de Zuckerberg como antagonista del universo superheroico es uno de los casting más perfectos del show." },

  // ── S22 ──
  "Dead Kids": { aired:"26 de septiembre de 2018", world:"Parkland había ocurrido en febrero de 2018. March for Our Lives había reunido millones. El debate continuaba igual.", controversy:"La normalización del tiroteo escolar representada como algo que la gente simplemente acepta fue dolorosamente precisa.", legacy:"Uno de los comentarios más oscuros y necesarios sobre la violencia armada en escuelas en la historia de la TV." },
  "The Problem with a Poo": { aired:"10 de octubre de 2018", world:"La cultura de la cancelación en Twitter estaba en su pico. Figuras públicas caían diariamente.", controversy:"Usar a Mr. Hankey como chivo expiatorio de la cancelación fue criticado por trivializar el movimiento.", legacy:"La sátira de la cancelación usando al excremento más icónico del show fue meta y brillante al mismo tiempo." },
  "Tegridy Farms": { aired:"17 de octubre de 2018", world:"Colorado había legalizado el cannabis recreacional en 2012. Los dispensarios proliferaban.", controversy:"Randy dejando Denver por la vida rural fue visto como una crítica al abandono urbano por parte de la clase media.", legacy:"Inició el arco de Tegridy Farms que definiría las últimas temporadas de la serie." },
  "Time To Get Cereal": { aired:"7 de noviembre de 2018", world:"El cambio climático era el tema político más urgente. El IPCC había emitido su informe más alarmante.", controversy:"El show se disculpó explícitamente por haber burlado a Al Gore en S10. Una de las raras autocríticas del programa.", legacy:"ManBearPig siendo real es uno de los mejores retcons de la serie. La humildad de Trey y Matt fue auténtica." },

  // ── S23 ──
  "Band in China": { aired:"2 de octubre de 2019", world:"Hollywood censurada activamente películas para el mercado chino. La NBA había tenido su escándalo con Hong Kong días antes.", controversy:"Comedy Central fue eliminado de la distribución en China inmediatamente. Trey y Matt lo celebraron públicamente.", legacy:"El episodio más valiente sobre la relación entre el entretenimiento americano y la censura china jamás producido." },
  "Shots!!!": { aired:"9 de octubre de 2019", world:"El movimiento antivacunas resurgía. Los brotes de sarampión aumentaban en EE.UU. por primera vez en décadas.", controversy:"Satirizar el movimiento antivacunas en 2019 fue perfecto timing. La pandemia de 2020 lo hizo más relevante.", legacy:"Envejeció perfectamente con la pandemia. Uno de los episodios más prescientes del show." },
  "Mexican Joker": { aired:"25 de septiembre de 2019", world:"Joker de Todd Phillips acababa de estrenar. Los centros de detención de ICE estaban en el centro del debate.", controversy:"La premisa de que el sistema de detención crearía un villano fue considerada tanto brillante como irresponsable.", legacy:"La doble sátira del sistema migratorio y la glorificación del villano cinematográfico es extraordinariamente precisa." },

  // ── S24 ──
  "The Pandemic Special": { aired:"30 de septiembre de 2020", world:"La pandemia de COVID-19 llevaba 6 meses. Los colegios cerrados, las mascarillas y el distanciamiento eran la nueva realidad.", controversy:"Fue emitido durante la pandemia activa. Algunas personas encontraron el humor inapropiado en ese contexto.", legacy:"El episodio producido más rápido en circunstancias más extremas. Una hazaña de producción y un documento histórico." },
  "South ParQ Vaccination Special": { aired:"10 de marzo de 2021", world:"Las vacunas COVID comenzaban a distribuirse. La lucha por conseguirlas era caótica. QAnon era un fenómeno masivo.", controversy:"Hacer que los profesores del colegio sean QAnon fue un ataque directo al movimiento en su pico de influencia.", legacy:"La más memorable de las producciones especiales de la pandemia. Captura perfectamente el caos vacunal." },

  // ── S25 ──
  "The Big Fix": { aired:"9 de febrero de 2022", world:"El debate sobre representación racial en los medios era el más activo de la década.", controversy:"El cambio de Token a Tolkien fue aplaudido por muchos como tardío pero necesario. Algunos lo consideraron un movimiento de PR.", legacy:"Uno de los cambios de nombre más significativos en la historia de la TV animada. Una decisión de producción real." },
  "Back To the Cold War": { aired:"2 de marzo de 2022", world:"Rusia invadía Ucrania días antes. La Guerra Fría parecía volver. Los bunkers y el miedo nuclear resurgían.", controversy:"La rapidez con que reaccionaron a la invasión ucraniana fue extraordinaria. El episodio se sentía urgente.", legacy:"El show mantuvo su tradición de reaccionar a eventos mundiales con una velocidad incomparable." },
  "Post Covid": { aired:"25 de noviembre de 2021", world:"Las primeras vacunas estaban disponibles. El mundo post-COVID comenzaba a tomar forma lentamente.", controversy:"Ver a los personajes adultos en un futuro sin Kenny fue emotivamente perturbador para los fans de largo aliento.", legacy:"El experimento narrativo más ambicioso del show en años. Ver a los personajes 40 años después fue revelador." },
  "City People": { aired:"23 de febrero de 2022", world:"La pandemia había vaciado las ciudades y llenado los suburbios rurales. La gentrificación rural era un fenómeno real.", controversy:"La tensión entre locales y recién llegados urbanos capturó perfectamente la crisis de la vivienda post-pandemia.", legacy:"Una de las mejores sátiras del show sobre las consecuencias no intencionadas de la pandemia en las comunidades rurales." },

  // ── S26 ──
  "Cupid Ye": { aired:"8 de febrero de 2023", world:"Kanye West había hecho declaraciones antisemitas públicas. Su caída cultural era el tema del momento.", controversy:"Conectar el amigo imaginario de Cartman con Kanye fue brillante pero también fue visto como una normalización.", legacy:"La integración de la caída de Kanye en la psicología de Cartman es uno de los mejores usos de un evento real." },
  "Joining the Panderverse": { aired:"27 de octubre de 2023", world:"Los debates sobre casting diverso en Hollywood eran los más polarizantes de la industria del entretenimiento.", controversy:"La crítica al 'pandering' fue acusada de ser conservadora por algunos, de ser precisa por otros.", legacy:"La parodia visual de Spider-Verse es técnicamente impresionante. El debate sobre representación sigue sin resolverse." },
  "Japanese Toilet": { aired:"15 de febrero de 2023", world:"Los inodoros japoneses Toto y Washlet se popularizaban en América. El mercado de baños de lujo explotaba.", controversy:"La obsesión de Randy con el inodoro como símbolo de status fue una crítica al consumismo de la clase media.", legacy:"Uno de los episodios más mundanos y absurdos de las últimas temporadas. Randy en su elemento consumista." },

  // ── S27 ──
  "Deep Learning": { aired:"2024", world:"ChatGPT había revolucionado el acceso a la inteligencia artificial. Todos usaban IA para todo en 2023-2024.", controversy:"El uso de IA para relaciones personales como Stan con Wendy captura perfectamente el debate sobre la autenticidad digital.", legacy:"El primer episodio en tratar la IA generativa como fenómeno cultural cotidiano. Extraordinariamente oportuno." },
  "Not Suitable for Children": { aired:"2024", world:"OnlyFans y el contenido para adultos en redes sociales era un debate educativo y legislativo activo.", controversy:"El pánico de los padres ante el acceso de menores a contenido adulto online fue retratado con exactitud dolorosa.", legacy:"Uno de los episodios más actuales sobre los desafíos de la crianza en la era digital." },

  // Contexto por defecto para episodios sin contexto específico
};

const getEpisodeContext = (title) => CONTEXTS[title] || null;
const TYPES_LIST = ["absurdo","dark","parodia","político","personaje","meta","épico","clásico","musical"];

const getBadge = (funny) => {
  if (funny >= 9.5) return { label:"OBRA MAESTRA", fg:"#F5C400", bg:"#7B1010", emoji:"🏆" };
  if (funny >= 9.0) return { label:"IMPRESCINDIBLE", fg:"#fff",    bg:"#CC1A1A", emoji:"🔥" };
  if (funny >= 8.5) return { label:"MUY GRACIOSO",   fg:"#1a1a1a", bg:"#F5C400", emoji:"😂" };
  if (funny >= 8.0) return { label:"SÓLIDO",          fg:"#fff",    bg:"#1A5276", emoji:"👍" };
  return               { label:"VALE LA PENA",    fg:"#fff",    bg:"#2E7B2E", emoji:"🙂" };
};

const store = {
  async get(key, fallback) {
    try { const r = localStorage.getItem(key); return r ? JSON.parse(r) : fallback; }
    catch { return fallback; }
  },
  async set(key, val) {
    try { localStorage.setItem(key, JSON.stringify(val)); } catch(e) {}
  }
};

function MeterBar({ value, max=10, color, label }) {
  const pct = (value/max)*100;
  return (
    <div style={{ display:"flex", gap:8, alignItems:"center", marginBottom:4 }}>
      <span style={{ fontFamily:"'Bangers',cursive", fontSize:11, color:"#555", minWidth:52, letterSpacing:1 }}>{label}</span>
      <div style={{ flex:1, height:8, background:"#e8e0d0", border:"2px solid #1a1a1a", borderRadius:2, overflow:"hidden" }}>
        <div style={{ width:`${pct}%`, height:"100%", background:color, transition:"width 0.9s cubic-bezier(.4,2,.6,1)" }} />
      </div>
      <span style={{ fontFamily:"'Bangers',cursive", fontSize:12, color:"#1a1a1a", minWidth:20, textAlign:"right" }}>{value}</span>
    </div>
  );
}

function StarRater({ title, ratings, onRate }) {
  const cur = ratings[title] || 0;
  return (
    <div style={{ display:"flex", gap:1 }}>
      {[1,2,3,4,5].map(n => (
        <button key={n} onClick={() => onRate(title, n)}
          style={{ background:"none", border:"none", cursor:"pointer", fontSize:18,
                   color:n<=cur?"#F5C400":"#ccc", padding:"0 2px",
                   textShadow:n<=cur?"0 0 1px #1a1a1a":"none", transition:"all 0.1s" }}>★</button>
      ))}
    </div>
  );
}

function Tag({ children, variant="char" }) {
  const styles = {
    char: { bg:"#CC1A1A", color:"#fff" },
    type: { bg:"#1a1a1a", color:"#F5C400" },
    auto: { bg:"#1A5276", color:"#fff" },
  };
  const s = styles[variant];
  return (
    <span style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:1,
                   padding:"2px 7px", background:s.bg, color:s.color,
                   border:"2px solid #1a1a1a", marginRight:4, marginBottom:4,
                   display:"inline-block", lineHeight:1.6 }}>
      {children}
    </span>
  );
}

function Btn({ onClick, children, variant="primary", disabled=false, small=false }) {
  const v = {
    primary:   { bg:"#CC1A1A", color:"#fff",    border:"#8B0000" },
    yellow:    { bg:"#F5C400", color:"#1a1a1a", border:"#B8920A" },
    navy:      { bg:"#1A5276", color:"#fff",    border:"#0d2d42" },
    ghost:     { bg:"#fff",    color:"#1a1a1a", border:"#1a1a1a" },
    purple:    { bg:"#6B21A8", color:"#fff",    border:"#4a1272" },
    dark:      { bg:"#1a1a1a", color:"#F5C400", border:"#000" },
  }[variant] || { bg:"#fff", color:"#1a1a1a", border:"#1a1a1a" };
  return (
    <button onClick={onClick} disabled={disabled}
      style={{ fontFamily:"'Bangers',cursive", letterSpacing:2,
               fontSize:small?12:15, padding:small?"6px 12px":"11px 20px",
               background:disabled?"#ccc":v.bg, color:disabled?"#888":v.color,
               border:`3px solid ${disabled?"#aaa":v.border}`,
               cursor:disabled?"default":"pointer",
               boxShadow:disabled?"none":`3px 3px 0 ${v.border}`,
               transition:"all 0.1s", lineHeight:1.3,
               transform:"none" }}
      onMouseDown={e => { if(!disabled) e.currentTarget.style.transform="translate(2px,2px)"; e.currentTarget.style.boxShadow="1px 1px 0 "+v.border; }}
      onMouseUp={e => { e.currentTarget.style.transform="none"; e.currentTarget.style.boxShadow=disabled?"none":`3px 3px 0 ${v.border}`; }}
    >
      {children}
    </button>
  );
}

function EpisodeCard({ ep, watched, favorites, ratings, onSkip, onWatched, onFav, onRate, compact=false, accentColor=null }) {
  const b = getBadge(ep.funny);
  const isWatched = watched.has(ep.title);
  const isFav = favorites.has(ep.title);
  const accent = accentColor || b.bg;
  const [showContext, setShowContext] = useState(false);
  const ctx = getEpisodeContext(ep.title);

  return (
    <div className="card-in" style={{
      background:"#FAFAF0", border:"3px solid #1a1a1a",
      borderRadius:6, padding:compact?"12px":"18px",
      boxShadow:"5px 5px 0 #1a1a1a", position:"relative",
      borderTop:`6px solid ${accent}`
    }}>
      {/* Badge + meta */}
      <div style={{ display:"flex", justifyContent:"space-between", alignItems:"flex-start", marginBottom:8, flexWrap:"wrap", gap:4 }}>
        <span style={{
          fontFamily:"'Bangers',cursive", fontSize:11, letterSpacing:2,
          background:b.bg, color:b.fg, padding:"2px 8px",
          border:"2px solid #1a1a1a", display:"inline-block"
        }}>{b.emoji} {b.label}</span>
        <div style={{ display:"flex", gap:4, alignItems:"center" }}>
          {ep.auto && <Tag variant="auto">AUTOCONTENIDO</Tag>}
          <span style={{ fontFamily:"'Bangers',cursive", fontSize:12, color:"#888", letterSpacing:1 }}>S{ep.s}·E{ep.e}</span>
        </div>
      </div>

      {/* Title */}
      <h2 style={{ margin:"0 0 10px", fontFamily:"'Bangers',cursive",
                   fontSize:compact?20:26, letterSpacing:2, color:"#1a1a1a",
                   lineHeight:1.1, textTransform:"uppercase" }}>{ep.title}</h2>

      {/* Tags */}
      <div style={{ marginBottom:10, lineHeight:1 }}>
        {ep.chars.map(c => <Tag key={c} variant="char">{c}</Tag>)}
        {ep.types.map(t => <Tag key={t} variant="type">{t}</Tag>)}
      </div>

      {/* Meters */}
      <div style={{ marginBottom:10 }}>
        <MeterBar value={ep.funny}  max={10} color={b.bg}    label="GRACIA"  />
        <MeterBar value={ep.dark}   max={10} color="#6B21A8" label="OSCURO"  />
        <MeterBar value={ep.impact} max={10} color="#CC1A1A" label="IMPACTO" />
      </div>

      {!compact && (
        <>
          <p style={{ margin:"0 0 10px", fontSize:13, color:"#333",
                      fontFamily:"'Nunito',sans-serif", lineHeight:1.65,
                      borderTop:"2px solid #e8e0d0", paddingTop:10 }}>{ep.desc}</p>
          <div style={{ padding:"8px 12px", background:"#1a1a1a", marginBottom:12, borderRadius:4 }}>
            <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, color:"#F5C400", marginBottom:2 }}>POR QUÉ VERLO</div>
            <p style={{ margin:0, fontSize:12, color:"#e8e0d0", fontFamily:"'Nunito',sans-serif", lineHeight:1.5 }}>{ep.why}</p>
          </div>

          {/* ── CONTEXTO HISTÓRICO ── */}
          {ctx && (
            <>
              <button onClick={() => setShowContext(s => !s)}
                style={{ width:"100%", marginBottom:8, padding:"8px 12px",
                         fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:2,
                         background:showContext?"#1A5276":"transparent",
                         color:showContext?"#fff":"#1A5276",
                         border:"2px solid #1A5276", borderRadius:4, cursor:"pointer",
                         display:"flex", justifyContent:"space-between", alignItems:"center" }}>
                <span>🌍 CONTEXTO HISTÓRICO</span>
                <span>{showContext?"▲":"▼"}</span>
              </button>

              {showContext && (
                <div style={{ background:"#EBF5FB", border:"2px solid #1A5276", borderRadius:4, padding:14, marginBottom:12, display:"flex", flexDirection:"column", gap:10 }}>
                  <div>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, color:"#1A5276", marginBottom:2 }}>📅 FECHA DE ESTRENO</div>
                    <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a" }}>{ctx.aired}</div>
                  </div>
                  <div>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, color:"#1A5276", marginBottom:2 }}>🌍 EL MUNDO EN ESE MOMENTO</div>
                    <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a", lineHeight:1.5 }}>{ctx.world}</div>
                  </div>
                  <div>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, color:"#CC1A1A", marginBottom:2 }}>🔥 POR QUÉ FUE POLÉMICO</div>
                    <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a", lineHeight:1.5 }}>{ctx.controversy}</div>
                  </div>
                  <div>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, color:"#2E7B2E", marginBottom:2 }}>⭐ LEGADO</div>
                    <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a", lineHeight:1.5 }}>{ctx.legacy}</div>
                  </div>
                </div>
              )}
            </>
          )}
        </>
      )}

      {/* Actions */}
      <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", borderTop:"2px solid #e8e0d0", paddingTop:10, flexWrap:"wrap", gap:6 }}>
        <StarRater title={ep.title} ratings={ratings} onRate={onRate} />
        <div style={{ display:"flex", gap:6, alignItems:"center" }}>
          {onSkip && <Btn onClick={onSkip} variant="ghost" small>SALTAR →</Btn>}
          <button onClick={() => onFav(ep.title)}
            style={{ background:"none", border:"none", cursor:"pointer",
                     fontSize:20, color:isFav?"#CC1A1A":"#ccc",
                     textShadow:isFav?"0 0 2px #8B0000":"none", padding:"0 2px" }}>♥</button>
          <Btn onClick={() => onWatched(ep.title)} variant={isWatched?"navy":"ghost"} small>
            {isWatched ? "VISTO ✓" : "MARCAR"}
          </Btn>
        </div>
      </div>
    </div>
  );
}

export default function App() {
  const [tab, setTab] = useState("ruleta");
  const [watched, setWatched] = useState(new Set());
  const [favorites, setFavorites] = useState(new Set());
  const [ratings, setRatings] = useState({});
  const [duelHistory, setDuelHistory] = useState([]);

  const [current, setCurrent] = useState(null);
  const [spinning, setSpinning] = useState(false);
  const [history, setHistory] = useState([]);
  const [showFilters, setShowFilters] = useState(false);
  const [filters, setFilters] = useState({ minFunny:7.5, char:"all", type:"all", autoOnly:false, hideWatched:false });

  const [duelPair, setDuelPair] = useState(null);
  const [listSort, setListSort] = useState("funny");
  const [listSearch, setListSearch] = useState("");

  const [surpriseEp, setSurpriseEp] = useState(null);
  const [surpriseLoading, setSurpriseLoading] = useState(false);
  const [surpriseReason, setSurpriseReason] = useState(null);

  const [marathon, setMarathon] = useState(null);
  const [marathonLoading, setMarathonLoading] = useState(false);
  const [marathonSize, setMarathonSize] = useState(4);
  const [marathonMode, setMarathonMode] = useState("variado"); // variado | oscuro | clasico | cartman | randy // "mios" | "comunidad"

  useEffect(() => {
    // Load Bangers + Nunito fonts
    const link = document.createElement("link");
    link.rel = "stylesheet";
    link.href = "https://fonts.googleapis.com/css2?family=Bangers&family=Nunito:wght@400;600;700&display=swap";
    document.head.appendChild(link);

    const style = document.createElement("style");
    style.textContent = `
      @keyframes diceSpin { 0%{transform:rotate(-15deg) scale(1)} 50%{transform:rotate(375deg) scale(1.6)} 100%{transform:rotate(720deg) scale(1)} }
      @keyframes cardIn { from{opacity:0;transform:translateY(20px) rotate(-1deg)} to{opacity:1;transform:translateY(0) rotate(0deg)} }
      @keyframes twinkle { 0%,100%{opacity:0.3} 50%{opacity:1} }
      @keyframes mountainFloat { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-3px)} }
      .spin-dice { animation: diceSpin 0.7s cubic-bezier(.4,2,.3,1) forwards; }
      .card-in { animation: cardIn 0.4s cubic-bezier(.4,2,.3,1) both; }
      ::-webkit-scrollbar { width:4px; }
      ::-webkit-scrollbar-thumb { background:#1a1a1a; border-radius:2px; }
      * { box-sizing: border-box; }
    `;
    document.head.appendChild(style);
    return () => { document.head.removeChild(link); document.head.removeChild(style); };
  }, []);

  useEffect(() => {
    (async () => {
      setWatched(new Set(await store.get("sp_watched", [])));
      setFavorites(new Set(await store.get("sp_favorites", [])));
      setRatings(await store.get("sp_ratings", {}));
      setDuelHistory(await store.get("sp_duel", []));
    })();
  }, []);

  const markWatched = async (title) => {
    const next = new Set(watched);
    next.has(title) ? next.delete(title) : next.add(title);
    setWatched(next);
    await store.set("sp_watched", [...next]);
  };

  const toggleFav = async (title) => {
    const next = new Set(favorites);
    const wasAlreadyFav = next.has(title);
    wasAlreadyFav ? next.delete(title) : next.add(title);
    setFavorites(next);
    await store.set("sp_favorites", [...next]);

  };
  const rate = async (title, stars) => {
    const next = { ...ratings, [title]: stars };
    setRatings(next);
    await store.set("sp_ratings", next);
  };

  const getPool = () => EPISODES.filter(ep => {
    if (ep.funny < filters.minFunny) return false;
    if (filters.char !== "all" && !ep.chars.includes(filters.char)) return false;
    if (filters.type !== "all" && !ep.types.includes(filters.type)) return false;
    if (filters.autoOnly && !ep.auto) return false;
    if (filters.hideWatched && watched.has(ep.title)) return false;
    return true;
  });

  // Weighted random: favorites 3x, high-rated 2x, duel winners 1.5x, unseen unwatched 1.2x, base 1x
  const weightedPick = (pool) => {
    const weighted = [];
    pool.forEach(ep => {
      const isFav = favorites.has(ep.title);
      const userRating = ratings[ep.title] || 0;
      const isDuelWinner = duelHistory.some(d => d.winner === ep.title);
      const isUnseen = !watched.has(ep.title);
      let w = 1;
      if (isFav) w *= 3;
      if (userRating >= 4) w *= 2;
      else if (userRating === 3) w *= 1.3;
      if (isDuelWinner) w *= 1.5;
      if (isUnseen) w *= 1.2;
      for (let i = 0; i < Math.ceil(w * 10); i++) weighted.push(ep);
    });
    // Fisher-Yates shuffle on weighted array then pick first
    for (let i = weighted.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [weighted[i], weighted[j]] = [weighted[j], weighted[i]];
    }
    return weighted[0];
  };

  const roll = () => {
    const pool = getPool().filter(e => e.id !== current?.id);
    if (!pool.length) return;
    setSpinning(true);
    setTimeout(() => { setCurrent(weightedPick(pool)); setSpinning(false); }, 700);
  };
  const skip = () => {
    const pool = getPool().filter(e => e.id !== current?.id);
    if (!pool.length) return;
    if (current) setHistory(h => [current, ...h].slice(0, 6));
    setCurrent(weightedPick(pool));
  };
  const newDuel = () => {
    const pool = EPISODES.filter(e => !watched.has(e.title));
    if (pool.length < 2) return;
    // Fisher-Yates shuffle
    const arr = [...pool];
    for (let i = arr.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
    setDuelPair([arr[0], arr[1]]);
  };
  const pickWinner = async (winner, loser) => {
    const next = [...duelHistory, { winner: winner.title, loser: loser.title }].slice(-50);
    setDuelHistory(next);
    await store.set("sp_duel", next);
    newDuel();
  };
  const getSortedList = () => {
    let list = [...EPISODES];
    if (listSearch) list = list.filter(e =>
      e.title.toLowerCase().includes(listSearch.toLowerCase()) ||
      e.chars.some(c => c.toLowerCase().includes(listSearch.toLowerCase())));
    return list.sort((a,b) => {
      if (listSort==="funny")  return b.funny-a.funny;
      if (listSort==="dark")   return b.dark-a.dark;
      if (listSort==="impact") return b.impact-a.impact;
      if (listSort==="season") return a.s-b.s || a.e-b.e;
      return 0;
    });
  };


  const getSurprise = async () => {
    setSurpriseLoading(true); setSurpriseEp(null); setSurpriseReason(null);
    const likedEps = EPISODES.filter(e => (ratings[e.title]||0)>=4 || favorites.has(e.title) || duelHistory.some(d => d.winner===e.title));
    let avgDark=5, avgFunny=8.8, preferredTypes=[], preferredChars=[];
    if (likedEps.length>0) {
      avgDark = likedEps.reduce((s,e)=>s+e.dark,0)/likedEps.length;
      avgFunny = likedEps.reduce((s,e)=>s+e.funny,0)/likedEps.length;
      const tc={}, cc={};
      likedEps.forEach(e => { e.types.forEach(t=>tc[t]=(tc[t]||0)+1); e.chars.forEach(c=>cc[c]=(cc[c]||0)+1); });
      preferredTypes = Object.entries(tc).sort((a,b)=>b[1]-a[1]).slice(0,2).map(x=>x[0]);
      preferredChars = Object.entries(cc).sort((a,b)=>b[1]-a[1]).slice(0,2).map(x=>x[0]);
    }
    const candidates = EPISODES.filter(e => !watched.has(e.title) && !favorites.has(e.title));
    if (!candidates.length) { setSurpriseLoading(false); return; }
    const scored = candidates.map(ep => {
      let score=0;
      score += Math.abs(ep.dark-avgDark)*1.5;
      score += Math.abs(ep.funny-avgFunny)*2;
      if (preferredTypes.length && !ep.types.some(t=>preferredTypes.includes(t))) score+=3;
      if (preferredChars.length && !ep.chars.some(c=>preferredChars.includes(c))) score+=2;
      return { ep, score };
    });
    scored.sort((a,b)=>b.score-a.score);
    const topN = scored.slice(0, Math.min(5, scored.length));
    const picked = topN[Math.floor(Math.random() * topN.length)].ep;
    setSurpriseEp(picked);
    const reasons = [
      `S${picked.s}E${picked.e} — completamente fuera de tu zona de confort habitual.`,
      `Con oscuridad ${picked.dark}/10 y gracia ${picked.funny}/10, este no es tu episodio típico.`,
      `${picked.chars[0]} protagoniza algo que probablemente no esperabas ver hoy.`,
    ];
    const warnings = [
      picked.dark >= 7 ? "⚠ Es bastante oscuro. Estás avisado." : "No es el más oscuro pero tampoco el más seguro.",
      picked.types.includes("político") ? "Crítica política pesada. Ideal para esta noche." : "Puro absurdismo. Preparate.",
      "Todo lo que creés saber sobre este episodio va a cambiar.",
    ];
    setSurpriseReason({
      reason: reasons[Math.floor(Math.random()*reasons.length)],
      warning: warnings[Math.floor(Math.random()*warnings.length)]
    });
    setSurpriseLoading(false);
  };

  const generateMarathon = async () => {
    setMarathonLoading(true);
    setMarathon(null);

    // Filter pool by mode
    let pool = EPISODES.filter(e => !watched.has(e.title));
    if (marathonMode === "oscuro")  pool = pool.filter(e => e.dark >= 6);
    if (marathonMode === "clasico") pool = pool.filter(e => e.s <= 10);
    if (marathonMode === "cartman") pool = pool.filter(e => e.chars.includes("Cartman"));
    if (marathonMode === "randy")   pool = pool.filter(e => e.chars.includes("Randy"));
    if (pool.length < marathonSize) pool = EPISODES; // fallback if too few

    // Fisher-Yates shuffle
    const arr = [...pool];
    for (let i = arr.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }

    // Pick ensuring variety: no two consecutive same type/char
    const picked = [];
    const remaining = [...arr];
    while (picked.length < marathonSize && remaining.length > 0) {
      const last = picked[picked.length - 1];
      const idx = remaining.findIndex(ep => {
        if (!last) return true;
        const sameType = ep.types.some(t => last.types.includes(t));
        const sameChar = ep.chars[0] === last.chars[0];
        return !sameType || !sameChar;
      });
      const pick = idx >= 0 ? remaining.splice(idx, 1)[0] : remaining.splice(0, 1)[0];
      picked.push(pick);
    }

    // Estimate total time (avg 22 min per episode)
    const totalMin = picked.length * 22;
    const hours = Math.floor(totalMin / 60);
    const mins = totalMin % 60;
    const timeStr = hours > 0 ? `${hours}h ${mins}min` : `${mins}min`;

    const avgDarkM = picked.reduce((s,e)=>s+e.dark,0)/picked.length;
    const avgFunnyM = picked.reduce((s,e)=>s+e.funny,0)/picked.length;
    const modeLabels = { variado:"NOCHE VARIADA DE SP", oscuro:"NOCHE OSCURA EN SOUTH PARK", clasico:"VIAJE AL PASADO", cartman:"LA NOCHE DE CARTMAN", randy:"LA NOCHE DE RANDY" };
    const vibes = {
      variado: "Una mezcla perfecta de humor, oscuridad y absurdismo.",
      oscuro: "Esta noche no apta para corazones débiles.",
      clasico: "Los clásicos que definieron la serie.",
      cartman: "Cartman en su máximo esplendor durante toda la noche.",
      randy: "Randy Marsh toma el control de la noche."
    };
    const aiTitle = modeLabels[marathonMode] || "NOCHE DE SOUTH PARK";
    const aiVibe = vibes[marathonMode] || "Una noche de South Park como pocas.";

    setMarathon({ episodes: picked, time: timeStr, aiTitle, aiVibe });
    setMarathonLoading(false);
  };

  const pool = getPool();
  const TABS = [
    { id:"ruleta",    icon:"🎲", label:"RULETA"  },
    { id:"duelo",     icon:"⚔️",  label:"DUELO"   },
    { id:"lista",     icon:"📋",  label:"LISTA"   },
    { id:"maraton",   icon:"📺",  label:"MARATÓN" },
    { id:"sorpresa",  icon:"😱",  label:"WTF"     },
    { id:"favoritos", icon:"♥",   label:"FAVS"    },
  ];

  // ── Stars background ──
  const stars = Array.from({length:40},(_,i)=>({
    x: (i*37+13)%100, y: (i*53+7)%60,
    size: i%3===0?2:1,
    delay: (i*0.3)%3
  }));

  const SectionTitle = ({children, sub}) => (
    <div style={{ textAlign:"center", marginBottom:16 }}>
      <h2 style={{ fontFamily:"'Bangers',cursive", fontSize:28, letterSpacing:3,
                   color:"#F5C400", margin:0, textShadow:"2px 2px 0 #1a1a1a, -1px -1px 0 #1a1a1a",
                   textTransform:"uppercase" }}>{children}</h2>
      {sub && <p style={{ fontFamily:"'Nunito',sans-serif", fontSize:11, color:"#aab", margin:"4px 0 0", letterSpacing:1 }}>{sub}</p>}
    </div>
  );

  const FilterPill = ({active, onClick, children, variant="yellow"}) => (
    <button onClick={onClick} style={{
      fontFamily:"'Bangers',cursive", fontSize:11, letterSpacing:1,
      padding:"4px 10px", cursor:"pointer",
      background:active?(variant==="yellow"?"#F5C400":"#CC1A1A"):"transparent",
      color:active?(variant==="yellow"?"#1a1a1a":"#fff"):"#aaa",
      border:`2px solid ${active?(variant==="yellow"?"#B8920A":"#8B0000"):"#555"}`,
      boxShadow:active?`2px 2px 0 ${variant==="yellow"?"#B8920A":"#8B0000"}`:"none",
      transition:"all 0.1s"
    }}>{children}</button>
  );

  return (
    <div style={{ minHeight:"100vh", background:"#0B1629", color:"#e8e0d0",
                  fontFamily:"'Nunito',sans-serif", paddingBottom:72, position:"relative", overflow:"hidden" }}>

      {/* ── Night sky stars ── */}
      <div style={{ position:"fixed", top:0, left:0, right:0, height:"100vh", pointerEvents:"none", zIndex:0 }}>
        {stars.map((s,i) => (
          <div key={i} style={{
            position:"absolute", left:`${s.x}%`, top:`${s.y}%`,
            width:s.size, height:s.size, borderRadius:"50%",
            background:"#fff", opacity:0.6,
            animation:`twinkle ${2+s.delay}s ease-in-out infinite`,
            animationDelay:`${s.delay}s`
          }} />
        ))}
      </div>

      {/* ── Header ── */}
      <div style={{ position:"relative", zIndex:1, textAlign:"center", padding:"18px 16px 0", background:"linear-gradient(180deg,#0B1629 60%,transparent)" }}>
        <div style={{ fontFamily:"'Bangers',cursive", fontSize:11, letterSpacing:8, color:"#F5C400",
                      textShadow:"1px 1px 0 #1a1a1a", marginBottom:2 }}>★ COLORADO ★</div>
        <h1 style={{ margin:"0 0 2px", fontFamily:"'Bangers',cursive",
                     fontSize:"clamp(30px,8vw,48px)", letterSpacing:4,
                     color:"#fff",
                     textShadow:"3px 3px 0 #CC1A1A, 5px 5px 0 #8B0000",
                     textTransform:"uppercase" }}>
          SOUTH PARK
        </h1>
        <div style={{ fontFamily:"'Bangers',cursive", fontSize:"clamp(14px,4vw,20px)", letterSpacing:6,
                      color:"#F5C400", textShadow:"1px 1px 0 #1a1a1a", marginBottom:8 }}>
          EPISODE ROULETTE
        </div>

        {/* Mountain silhouette SVG */}
        <svg viewBox="0 0 400 60" style={{ width:"100%", maxWidth:520, display:"block", margin:"0 auto", marginBottom:-2 }}>
          <polygon points="0,60 40,20 80,40 130,5 180,35 220,10 270,38 310,15 360,32 400,18 400,60" fill="#142236" />
          <polygon points="0,60 30,30 60,45 100,15 145,42 180,22 215,45 250,28 290,48 330,20 370,38 400,28 400,60" fill="#0B1629" />
          {/* Snow caps */}
          <polygon points="130,5 118,20 142,20" fill="#e8f4f8" opacity="0.8"/>
          <polygon points="220,10 209,23 231,23" fill="#e8f4f8" opacity="0.8"/>
          <polygon points="310,15 300,26 320,26" fill="#e8f4f8" opacity="0.7"/>
        </svg>

        {/* Stats bar */}
        <div style={{ background:"#142236", borderTop:"3px solid #1a1a1a", borderBottom:"3px solid #1a1a1a",
                      padding:"6px 0", display:"flex", justifyContent:"center", gap:20 }}>
          {[
            [`${[...watched].length}`, "VISTOS"],
            [`${[...favorites].length}`, "FAVS"],
            [`${EPISODES.length}`, "EPS"],
            [`${Object.keys(ratings).length}`, "RATEDS"],
          ].map(([val,lab]) => (
            <div key={lab} style={{ textAlign:"center" }}>
              <div style={{ fontFamily:"'Bangers',cursive", fontSize:16, color:"#F5C400", letterSpacing:1, lineHeight:1 }}>{val}</div>
              <div style={{ fontFamily:"'Bangers',cursive", fontSize:9, color:"#556", letterSpacing:2 }}>{lab}</div>
            </div>
          ))}
        </div>
      </div>

      {/* ── Content ── */}
      <div style={{ position:"relative", zIndex:1, padding:"16px", maxWidth:520, margin:"0 auto" }}>

        {/* ── RULETA ── */}
        {tab === "ruleta" && (
          <div style={{ display:"flex", flexDirection:"column", gap:14 }}>
            <SectionTitle sub={`${pool.length} episodios en el pool`}>🎲 TIRAR EL DADO</SectionTitle>

            <div style={{ display:"flex", gap:8 }}>
              <button onClick={roll}
                style={{ flex:1, fontFamily:"'Bangers',cursive", fontSize:20, letterSpacing:4,
                         padding:"14px", background:"#CC1A1A", color:"#fff",
                         border:"3px solid #8B0000", boxShadow:"4px 4px 0 #8B0000",
                         cursor:"pointer", textTransform:"uppercase",
                         transition:"all 0.1s" }}
                onMouseDown={e=>{e.currentTarget.style.transform="translate(3px,3px)";e.currentTarget.style.boxShadow="1px 1px 0 #8B0000";}}
                onMouseUp={e=>{e.currentTarget.style.transform="none";e.currentTarget.style.boxShadow="4px 4px 0 #8B0000";}}
              >
                <span className={spinning?"spin-dice":""} style={{ display:"inline-block", marginRight:8 }}>🎲</span>
                TIRAR
              </button>
              <button onClick={() => setShowFilters(!showFilters)}
                style={{ padding:"14px 16px", fontFamily:"'Bangers',cursive", fontSize:18,
                         background:showFilters?"#F5C400":"#142236",
                         color:showFilters?"#1a1a1a":"#F5C400",
                         border:`3px solid ${showFilters?"#B8920A":"#2a4060"}`,
                         boxShadow:`3px 3px 0 ${showFilters?"#B8920A":"#0a1020"}`,
                         cursor:"pointer" }}>⚙</button>
            </div>

            {showFilters && (
              <div style={{ background:"#FAFAF0", border:"3px solid #1a1a1a",
                            borderRadius:4, padding:16, boxShadow:"4px 4px 0 #1a1a1a",
                            display:"flex", flexDirection:"column", gap:12 }}>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:14, letterSpacing:3, color:"#1a1a1a", borderBottom:"2px solid #1a1a1a", paddingBottom:6 }}>
                  ⚙ FILTROS
                </div>
                <div>
                  <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, color:"#555", marginBottom:6, letterSpacing:2 }}>
                    GRACIA MÍNIMA: <span style={{ color:"#CC1A1A" }}>{filters.minFunny}</span>
                  </div>
                  <input type="range" min={7.5} max={9.8} step={0.1} value={filters.minFunny}
                    onChange={e => setFilters(f => ({ ...f, minFunny:parseFloat(e.target.value) }))}
                    style={{ width:"100%", accentColor:"#CC1A1A", height:6 }} />
                </div>
                <div>
                  <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, color:"#555", marginBottom:6, letterSpacing:2 }}>PERSONAJE</div>
                  <div style={{ display:"flex", gap:5, flexWrap:"wrap" }}>
                    {["all",...CHARS_LIST].map(c => (
                      <FilterPill key={c} active={filters.char===c} onClick={() => setFilters(f=>({...f,char:c}))}>
                        {c==="all"?"TODOS":c.toUpperCase()}
                      </FilterPill>
                    ))}
                  </div>
                </div>
                <div>
                  <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, color:"#555", marginBottom:6, letterSpacing:2 }}>TIPO DE HUMOR</div>
                  <div style={{ display:"flex", gap:5, flexWrap:"wrap" }}>
                    {["all",...TYPES_LIST].map(t => (
                      <FilterPill key={t} variant="red" active={filters.type===t} onClick={() => setFilters(f=>({...f,type:t}))}>
                        {t==="all"?"TODOS":t.toUpperCase()}
                      </FilterPill>
                    ))}
                  </div>
                </div>
                <div style={{ display:"flex", gap:8 }}>
                  {[{k:"autoOnly",l:"SOLO AUTOCONTENIDOS"},{k:"hideWatched",l:"OCULTAR VISTOS"}].map(({k,l}) => (
                    <FilterPill key={k} active={filters[k]} onClick={() => setFilters(f=>({...f,[k]:!f[k]}))}>
                      {filters[k]?"✓ ":""}{l}
                    </FilterPill>
                  ))}
                </div>
              </div>
            )}

            {spinning && (
              <div style={{ textAlign:"center", padding:"40px 0" }}>
                <span className="spin-dice" style={{ display:"inline-block", fontSize:48 }}>🎲</span>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:14, letterSpacing:4, color:"#F5C400", marginTop:8 }}>TIRANDO...</div>
              </div>
            )}

            {!spinning && current && (
              <EpisodeCard ep={current} watched={watched} favorites={favorites}
                ratings={ratings} onSkip={skip} onWatched={markWatched}
                onFav={toggleFav} onRate={rate} />
            )}

            {!spinning && !current && (
              <div style={{ textAlign:"center", padding:"40px 0" }}>
                <div style={{ fontSize:40, marginBottom:8 }}>👆</div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:16, letterSpacing:3, color:"#556" }}>TIRÁ EL DADO PARA EMPEZAR</div>
              </div>
            )}

            {history.length > 0 && (
              <div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:11, letterSpacing:3, color:"#556", marginBottom:8 }}>
                  ↩ SALTADOS (TAP PARA RECUPERAR)
                </div>
                {history.map((ep,i) => {
                  const b = getBadge(ep.funny);
                  return (
                    <div key={i} onClick={() => setCurrent(ep)}
                      style={{ display:"flex", justifyContent:"space-between", alignItems:"center",
                               padding:"8px 12px", background:"#FAFAF0",
                               border:"2px solid #1a1a1a", marginBottom:4, cursor:"pointer",
                               boxShadow:"2px 2px 0 #1a1a1a" }}>
                      <span style={{ fontFamily:"'Bangers',cursive", fontSize:14, letterSpacing:1, color:"#1a1a1a" }}>{ep.title}</span>
                      <span style={{ fontFamily:"'Bangers',cursive", fontSize:12, background:b.bg, color:b.fg, padding:"1px 6px", border:"2px solid #1a1a1a" }}>{ep.funny}</span>
                    </div>
                  );
                })}
              </div>
            )}
          </div>
        )}

        {/* ── DUELO ── */}
        {tab === "duelo" && (
          <div style={{ display:"flex", flexDirection:"column", gap:14 }}>
            <SectionTitle sub="Tus elecciones alimentan la IA">⚔️ DUELO DE EPISODIOS</SectionTitle>
            {!duelPair ? (
              <div style={{ textAlign:"center" }}>
                <div style={{ fontSize:48, marginBottom:12 }}>⚔️</div>
                <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#aab", marginBottom:16, lineHeight:1.6 }}>
                  Te mostramos dos episodios.<br/>Vos elegís cuál verías primero.
                </div>
                <Btn onClick={newDuel} variant="yellow">⚔️ INICIAR DUELO</Btn>
              </div>
            ) : (
              <>
                {duelPair.map((ep, i) => (
                  <div key={ep.id}>
                    <EpisodeCard ep={ep} watched={watched} favorites={favorites}
                      ratings={ratings} onWatched={markWatched} onFav={toggleFav} onRate={rate} compact />
                    <button onClick={() => pickWinner(ep, duelPair[1-i])}
                      style={{ width:"100%", marginTop:8, padding:"12px",
                               fontFamily:"'Bangers',cursive", fontSize:16, letterSpacing:3,
                               background:"#F5C400", color:"#1a1a1a",
                               border:"3px solid #B8920A", boxShadow:"3px 3px 0 #B8920A",
                               cursor:"pointer" }}>
                      ✓ ELEGIRÍA ESTE
                    </button>
                    {i === 0 && (
                      <div style={{ textAlign:"center", padding:"12px 0",
                                    fontFamily:"'Bangers',cursive", fontSize:28, letterSpacing:6,
                                    color:"#CC1A1A", textShadow:"2px 2px 0 #8B0000" }}>VS</div>
                    )}
                  </div>
                ))}
                <div style={{ textAlign:"center" }}>
                  <Btn onClick={newDuel} variant="ghost" small>OTRO PAR →</Btn>
                </div>
              </>
            )}
            {duelHistory.length > 0 && (
              <div style={{ textAlign:"center", fontFamily:"'Bangers',cursive", fontSize:12, color:"#556", letterSpacing:2 }}>
                {duelHistory.length} DUELOS REGISTRADOS
              </div>
            )}
          </div>
        )}

        {/* ── LISTA ── */}
        {tab === "lista" && (
          <div style={{ display:"flex", flexDirection:"column", gap:10 }}>
            <SectionTitle sub={`${getSortedList().length} episodios`}>📋 TODOS LOS EPISODIOS</SectionTitle>
            <input value={listSearch} onChange={e => setListSearch(e.target.value)}
              placeholder="Buscar episodio o personaje..."
              style={{ padding:"10px 14px", background:"#FAFAF0",
                       border:"3px solid #1a1a1a", borderRadius:4,
                       fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a",
                       outline:"none", boxShadow:"3px 3px 0 #1a1a1a" }} />
            <div style={{ display:"flex", gap:6, flexWrap:"wrap" }}>
              {[["funny","GRACIA"],["dark","OSCURIDAD"],["impact","IMPACTO"],["season","TEMPORADA"]].map(([k,l]) => (
                <FilterPill key={k} active={listSort===k} onClick={() => setListSort(k)}>{l}</FilterPill>
              ))}
            </div>
            {getSortedList().map(ep => {
              const b = getBadge(ep.funny);
              const isW = watched.has(ep.title);
              const val = listSort==="dark"?ep.dark:listSort==="impact"?ep.impact:ep.funny;
              return (
                <div key={ep.id}
                  style={{ display:"flex", alignItems:"center", gap:10,
                           padding:"10px 12px", background: isW?"#e0e8d8":"#FAFAF0",
                           border:"2px solid #1a1a1a", borderRadius:4,
                           boxShadow:"2px 2px 0 #1a1a1a", opacity:isW?0.55:1 }}>
                  <span style={{ background:b.bg, color:b.fg, fontFamily:"'Bangers',cursive",
                                 fontSize:13, padding:"1px 6px", border:"2px solid #1a1a1a",
                                 minWidth:36, textAlign:"center" }}>{val}</span>
                  <div style={{ flex:1, minWidth:0 }}>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:15, letterSpacing:1,
                                  color:"#1a1a1a", whiteSpace:"nowrap", overflow:"hidden", textOverflow:"ellipsis" }}>{ep.title}</div>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, color:"#888", letterSpacing:1 }}>S{ep.s}·E{ep.e} · {ep.chars[0]}</div>
                  </div>
                  <button onClick={() => toggleFav(ep.title)}
                    style={{ background:"none", border:"none", cursor:"pointer",
                             fontSize:16, color:favorites.has(ep.title)?"#CC1A1A":"#ccc", padding:"0 2px" }}>♥</button>
                  <button onClick={() => markWatched(ep.title)}
                    style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:1,
                             padding:"3px 8px", cursor:"pointer",
                             background:isW?"#1A5276":"transparent",
                             color:isW?"#fff":"#888",
                             border:`2px solid ${isW?"#0d2d42":"#ccc"}` }}>
                    {isW?"✓":"○"}
                  </button>
                </div>
              );
            })}
          </div>
        )}

        {/* ── MARATÓN ── */}
        {tab === "maraton" && (
          <div style={{ display:"flex", flexDirection:"column", gap:14 }}>
            <SectionTitle sub="Generá una noche perfecta de South Park">📺 MODO MARATÓN</SectionTitle>

            {/* Config panel */}
            <div style={{ background:"#FAFAF0", border:"3px solid #1a1a1a", borderRadius:4, padding:16, boxShadow:"4px 4px 0 #1a1a1a", display:"flex", flexDirection:"column", gap:12 }}>
              {/* Cantidad */}
              <div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:2, color:"#555", marginBottom:6 }}>
                  CANTIDAD DE EPISODIOS: <span style={{ color:"#CC1A1A" }}>{marathonSize}</span>
                  <span style={{ color:"#888", fontSize:10 }}> (~{marathonSize * 22} min)</span>
                </div>
                <div style={{ display:"flex", gap:6 }}>
                  {[3,4,5,6].map(n => (
                    <button key={n} onClick={() => setMarathonSize(n)}
                      style={{ flex:1, padding:"8px", fontFamily:"'Bangers',cursive", fontSize:15, letterSpacing:1,
                               background:marathonSize===n?"#CC1A1A":"transparent",
                               color:marathonSize===n?"#fff":"#1a1a1a",
                               border:`3px solid ${marathonSize===n?"#8B0000":"#1a1a1a"}`,
                               boxShadow:marathonSize===n?"2px 2px 0 #8B0000":"2px 2px 0 #1a1a1a",
                               cursor:"pointer" }}>{n}</button>
                  ))}
                </div>
              </div>
              {/* Modo */}
              <div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:2, color:"#555", marginBottom:6 }}>MODO</div>
                <div style={{ display:"flex", gap:5, flexWrap:"wrap" }}>
                  {[["variado","🎲 VARIADO"],["oscuro","💀 DARK"],["clasico","⭐ CLÁSICOS (S1-10)"],["cartman","😈 CARTMAN"],["randy","🍺 RANDY"]].map(([id,label]) => (
                    <button key={id} onClick={() => setMarathonMode(id)}
                      style={{ padding:"6px 10px", fontFamily:"'Bangers',cursive", fontSize:11, letterSpacing:1,
                               background:marathonMode===id?"#1a1a1a":"transparent",
                               color:marathonMode===id?"#F5C400":"#1a1a1a",
                               border:`2px solid ${marathonMode===id?"#000":"#1a1a1a"}`,
                               boxShadow:marathonMode===id?"2px 2px 0 #000":"none",
                               cursor:"pointer" }}>{label}</button>
                  ))}
                </div>
              </div>
            </div>

            {/* Generate button */}
            <button onClick={generateMarathon} disabled={marathonLoading}
              style={{ padding:"16px", fontFamily:"'Bangers',cursive", fontSize:20, letterSpacing:4,
                       background:marathonLoading?"#333":"#CC1A1A", color:marathonLoading?"#666":"#fff",
                       border:`3px solid ${marathonLoading?"#222":"#8B0000"}`,
                       boxShadow:marathonLoading?"none":"5px 5px 0 #8B0000",
                       cursor:marathonLoading?"default":"pointer" }}>
              {marathonLoading ? "ARMANDO LA NOCHE..." : "📺 GENERAR MARATÓN"}
            </button>

            {/* Result */}
            {marathon && !marathonLoading && (
              <div style={{ display:"flex", flexDirection:"column", gap:10 }}>
                {/* Header */}
                <div style={{ background:"#1a1a1a", border:"3px solid #F5C400", borderRadius:4, padding:"14px 16px", boxShadow:"4px 4px 0 #B8920A" }}>
                  <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:3, color:"#F5C400", marginBottom:4 }}>📺 MARATÓN DE HOY</div>
                  <div style={{ fontFamily:"'Bangers',cursive", fontSize:22, letterSpacing:2, color:"#fff", marginBottom:4 }}>
                    {marathon.aiTitle || "NOCHE DE SOUTH PARK"}
                  </div>
                  {marathon.aiVibe && <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:12, color:"#aaa", marginBottom:8 }}>{marathon.aiVibe}</div>}
                  <div style={{ display:"flex", gap:12 }}>
                    <span style={{ fontFamily:"'Bangers',cursive", fontSize:13, color:"#F5C400" }}>⏱ {marathon.time}</span>
                    <span style={{ fontFamily:"'Bangers',cursive", fontSize:13, color:"#F5C400" }}>📺 {marathon.episodes.length} EPS</span>
                  </div>
                </div>

                {/* Episode list */}
                {marathon.episodes.map((ep, i) => {
                  const b = getBadge(ep.funny);
                  return (
                    <div key={ep.id} style={{ background:"#FAFAF0", border:"3px solid #1a1a1a", borderRadius:4, overflow:"hidden", boxShadow:"3px 3px 0 #1a1a1a" }}>
                      {/* Order bar */}
                      <div style={{ background:b.bg, padding:"4px 12px", display:"flex", justifyContent:"space-between", alignItems:"center" }}>
                        <span style={{ fontFamily:"'Bangers',cursive", fontSize:13, letterSpacing:2, color:b.fg }}>#{i+1} — {b.emoji} {b.label}</span>
                        <span style={{ fontFamily:"'Bangers',cursive", fontSize:11, color:b.fg, opacity:0.8 }}>S{ep.s}·E{ep.e} · ~22min</span>
                      </div>
                      <div style={{ padding:"12px 14px" }}>
                        <div style={{ fontFamily:"'Bangers',cursive", fontSize:19, letterSpacing:1, color:"#1a1a1a", marginBottom:5 }}>{ep.title}</div>
                        <div style={{ marginBottom:8 }}>
                          {ep.chars.map(c => <Tag key={c} variant="char">{c}</Tag>)}
                          {ep.types.map(t => <Tag key={t} variant="type">{t}</Tag>)}
                        </div>
                        <p style={{ margin:"0 0 10px", fontFamily:"'Nunito',sans-serif", fontSize:12, color:"#555", lineHeight:1.5 }}>{ep.desc}</p>
                        <div style={{ marginBottom:8 }}>
                          <MeterBar value={ep.funny}  max={10} color={b.bg}    label="GRACIA"  />
                          <MeterBar value={ep.dark}   max={10} color="#6B21A8" label="OSCURO"  />
                          <MeterBar value={ep.impact} max={10} color="#CC1A1A" label="IMPACTO" />
                        </div>
                        <div style={{ display:"flex", gap:6, justifyContent:"flex-end", borderTop:"2px solid #e8e0d0", paddingTop:8 }}>
                          <StarRater title={ep.title} ratings={ratings} onRate={rate} />
                          <button onClick={() => toggleFav(ep.title)}
                            style={{ background:"none", border:"none", cursor:"pointer", fontSize:18, color:favorites.has(ep.title)?"#CC1A1A":"#ccc" }}>♥</button>
                          <Btn onClick={() => markWatched(ep.title)} variant={watched.has(ep.title)?"navy":"ghost"} small>
                            {watched.has(ep.title)?"VISTO ✓":"MARCAR"}
                          </Btn>
                        </div>
                      </div>
                    </div>
                  );
                })}

                {/* Regenerate */}
                <div style={{ textAlign:"center" }}>
                  <Btn onClick={generateMarathon} variant="dark">OTRA MARATÓN →</Btn>
                </div>
              </div>
            )}

            {!marathon && !marathonLoading && (
              <div style={{ background:"#142236", border:"2px solid #2a4060", borderRadius:4, padding:"24px", textAlign:"center" }}>
                <div style={{ fontSize:32, marginBottom:8 }}>📺</div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:2, color:"#556", lineHeight:2 }}>
                  ELEGÍ EL MODO Y LA CANTIDAD<br/>
                  <span style={{ fontSize:10, color:"#444" }}>LA IA NOMBRA TU NOCHE</span>
                </div>
              </div>
            )}
          </div>
        )}

        {/* ── SORPRESA ── */}
        {tab === "sorpresa" && (
          <div style={{ display:"flex", flexDirection:"column", gap:14 }}>
            <SectionTitle sub="Ignora tus filtros. Sale lo que menos esperás.">😱 SORPRÉNDEME</SectionTitle>

            <button onClick={getSurprise} disabled={surpriseLoading}
              style={{ padding:"16px", fontFamily:"'Bangers',cursive", fontSize:22, letterSpacing:4,
                       background:surpriseLoading?"#333":"#6B21A8", color:surpriseLoading?"#666":"#fff",
                       border:`3px solid ${surpriseLoading?"#222":"#4a1272"}`,
                       boxShadow:surpriseLoading?"none":"5px 5px 0 #4a1272",
                       cursor:surpriseLoading?"default":"pointer",
                       textTransform:"uppercase" }}>
              {surpriseLoading ? "CALCULANDO WILDCARD..." : "😱 SORPRÉNDEME"}
            </button>

            {surpriseLoading && (
              <div style={{ textAlign:"center", padding:"30px 0" }}>
                <div style={{ fontSize:36, marginBottom:8 }}>🎲</div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:13, letterSpacing:3, color:"#6B21A8" }}>
                  ANALIZANDO TU ZONA DE CONFORT...
                </div>
              </div>
            )}

            {surpriseEp && !surpriseLoading && (() => {
              const b = getBadge(surpriseEp.funny);
              return (
                <div style={{ display:"flex", flexDirection:"column", gap:10 }}>
                  <div style={{ background:"#FAFAF0", border:"3px solid #6B21A8",
                                borderRadius:4, padding:"10px 14px", textAlign:"center",
                                boxShadow:"4px 4px 0 #4a1272" }}>
                    <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:3, color:"#6B21A8" }}>
                      ★ WILDCARD SELECCIONADO ★
                    </div>
                    <div style={{ fontFamily:"'Nunito',sans-serif", fontSize:11, color:"#888", marginTop:2 }}>
                      Lo más diferente a lo que normalmente elegís
                    </div>
                  </div>

                  <EpisodeCard ep={surpriseEp} watched={watched} favorites={favorites}
                    ratings={ratings} onWatched={markWatched} onFav={toggleFav} onRate={rate}
                    accentColor="#6B21A8" />

                  {surpriseReason && (
                    <div style={{ display:"flex", flexDirection:"column", gap:8 }}>
                      <div style={{ background:"#FAFAF0", border:"3px solid #6B21A8",
                                    borderRadius:4, padding:"12px 14px",
                                    boxShadow:"3px 3px 0 #4a1272" }}>
                        <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:3, color:"#6B21A8", marginBottom:4 }}>
                          POR QUÉ ES UNA SORPRESA
                        </div>
                        <p style={{ margin:0, fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a", lineHeight:1.5 }}>
                          {surpriseReason.reason}
                        </p>
                      </div>
                      {surpriseReason.warning && (
                        <div style={{ background:"#FAFAF0", border:"3px solid #CC1A1A",
                                      borderRadius:4, padding:"12px 14px",
                                      boxShadow:"3px 3px 0 #8B0000" }}>
                          <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:3, color:"#CC1A1A", marginBottom:4 }}>
                            ⚠ ADVERTENCIA
                          </div>
                          <p style={{ margin:0, fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#1a1a1a", lineHeight:1.5 }}>
                            {surpriseReason.warning}
                          </p>
                        </div>
                      )}
                    </div>
                  )}

                  <div style={{ textAlign:"center" }}>
                    <Btn onClick={getSurprise} variant="purple">OTRO WILDCARD →</Btn>
                  </div>
                </div>
              );
            })()}

            {!surpriseEp && !surpriseLoading && (
              <div style={{ background:"#142236", border:"2px solid #2a4060", borderRadius:4, padding:"20px", textAlign:"center" }}>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:12, letterSpacing:2, color:"#556", lineHeight:2.2 }}>
                  CUANTO MÁS USES LA APP<br/>MÁS PRECISA SERÁ LA SORPRESA<br/>
                  <span style={{ color:"#F5C400" }}>★</span> CALIFICÁ · <span style={{ color:"#CC1A1A" }}>♥</span> FAVORITOS · <span style={{ color:"#fff" }}>⚔️</span> DUELOS
                </div>
              </div>
            )}
          </div>
        )}

        {/* ── FAVORITOS ── */}
        {tab === "favoritos" && (
          <div style={{ display:"flex", flexDirection:"column", gap:14 }}>
            <SectionTitle sub={`${[...favorites].length} episodios guardados`}>♥ FAVORITOS</SectionTitle>

            {[...favorites].length === 0 ? (
              <div style={{ background:"#142236", border:"2px solid #2a4060", borderRadius:4, padding:"32px 20px", textAlign:"center" }}>
                <div style={{ fontSize:40, marginBottom:12 }}>♥</div>
                <div style={{ fontFamily:"'Bangers',cursive", fontSize:16, letterSpacing:3, color:"#556", lineHeight:2 }}>
                  AÚN NO TENÉS FAVORITOS<br/>
                  <span style={{ fontSize:12, color:"#444" }}>TOCÁ ♥ EN CUALQUIER EPISODIO</span>
                </div>
              </div>
            ) : (
              <>
                {/* Stats personales */}
                <div style={{ background:"#FAFAF0", border:"3px solid #1a1a1a", borderRadius:4, padding:"12px 16px", boxShadow:"3px 3px 0 #1a1a1a" }}>
                  {(() => {
                    const favEps = EPISODES.filter(e => favorites.has(e.title));
                    const avg = (favEps.reduce((s,e)=>s+e.funny,0)/favEps.length).toFixed(1);
                    const topChar = (() => { const cc={}; favEps.forEach(e=>e.chars.forEach(c=>cc[c]=(cc[c]||0)+1)); return Object.entries(cc).sort((a,b)=>b[1]-a[1])[0]?.[0]||"—"; })();
                    const topType = (() => { const tc={}; favEps.forEach(e=>e.types.forEach(t=>tc[t]=(tc[t]||0)+1)); return Object.entries(tc).sort((a,b)=>b[1]-a[1])[0]?.[0]||"—"; })();
                    return (
                      <div style={{ display:"flex", justifyContent:"space-around" }}>
                        {[[avg,"GRACIA PROM","★"],[topChar,"PERSONAJE","🎭"],[topType,"TIPO","🎬"]].map(([val,lab,icon]) => (
                          <div key={lab} style={{ textAlign:"center" }}>
                            <div style={{ fontFamily:"'Bangers',cursive", fontSize:16, color:"#CC1A1A", lineHeight:1.2 }}>{icon} {val}</div>
                            <div style={{ fontFamily:"'Bangers',cursive", fontSize:9, letterSpacing:2, color:"#888" }}>{lab}</div>
                          </div>
                        ))}
                      </div>
                    );
                  })()}
                </div>

                {/* Lista */}
                {EPISODES.filter(e => favorites.has(e.title)).map(ep => {
                  const b = getBadge(ep.funny);
                  return (
                    <div key={ep.id} style={{ background:"#FAFAF0", border:"3px solid #1a1a1a", borderRadius:4, padding:"14px", boxShadow:"4px 4px 0 #1a1a1a", borderTop:`6px solid ${b.bg}` }}>
                      <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:8 }}>
                        <span style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, background:b.bg, color:b.fg, padding:"2px 8px", border:"2px solid #1a1a1a" }}>
                          {b.emoji} {b.label}
                        </span>
                        <span style={{ fontFamily:"'Bangers',cursive", fontSize:11, color:"#888" }}>S{ep.s}·E{ep.e}</span>
                      </div>
                      <h3 style={{ margin:"0 0 8px", fontFamily:"'Bangers',cursive", fontSize:22, letterSpacing:2, color:"#1a1a1a", textTransform:"uppercase", lineHeight:1.1 }}>{ep.title}</h3>
                      <div style={{ marginBottom:8 }}>
                        {ep.chars.map(c => <Tag key={c} variant="char">{c}</Tag>)}
                        {ep.types.map(t => <Tag key={t} variant="type">{t}</Tag>)}
                      </div>
                      <p style={{ margin:"0 0 10px", fontFamily:"'Nunito',sans-serif", fontSize:13, color:"#333", lineHeight:1.6, borderTop:"2px solid #e8e0d0", paddingTop:8 }}>{ep.desc}</p>
                      <div style={{ marginBottom:10 }}>
                        <MeterBar value={ep.funny}  max={10} color={b.bg}    label="GRACIA"  />
                        <MeterBar value={ep.dark}   max={10} color="#6B21A8" label="OSCURO"  />
                        <MeterBar value={ep.impact} max={10} color="#CC1A1A" label="IMPACTO" />
                      </div>
                      <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", borderTop:"2px solid #e8e0d0", paddingTop:10 }}>
                        <StarRater title={ep.title} ratings={ratings} onRate={rate} />
                        <div style={{ display:"flex", gap:6, alignItems:"center" }}>
                          <Btn onClick={() => { setCurrent(ep); setTab("ruleta"); }} variant="primary" small>VER EN RULETA</Btn>
                          <button onClick={() => toggleFav(ep.title)} style={{ background:"none", border:"none", cursor:"pointer", fontSize:20, color:"#CC1A1A", padding:"0 2px" }}>♥</button>
                        </div>
                      </div>
                    </div>
                  );
                })}

                <div style={{ textAlign:"center", paddingTop:4 }}>
                  <div style={{ fontFamily:"'Bangers',cursive", fontSize:10, letterSpacing:2, color:"#444" }}>
                    {[...favorites].length} EPISODIO{[...favorites].length!==1?"S":""} GUARDADOS
                  </div>
                </div>
              </>
            )}
          </div>
        )}
      </div>

      {/* ── Bottom Nav ── */}
      <div style={{ position:"fixed", bottom:0, left:0, right:0, zIndex:10,
                    background:"#0B1629", borderTop:"3px solid #1a1a1a",
                    display:"flex" }}>
        {TABS.map(t => (
          <button key={t.id} onClick={() => setTab(t.id)}
            style={{ flex:1, background:tab===t.id?"#CC1A1A":"transparent",
                     border:"none", borderRight:"2px solid #1a1a1a",
                     cursor:"pointer", padding:"8px 4px 10px",
                     display:"flex", flexDirection:"column", alignItems:"center", gap:1,
                     transition:"background 0.15s" }}>
            <span style={{ fontSize:16 }}>{t.icon}</span>
            <span style={{ fontFamily:"'Bangers',cursive", fontSize:8, letterSpacing:1,
                           color:tab===t.id?"#fff":"#556" }}>{t.label}</span>
          </button>
        ))}
      </div>
    </div>
  );
}
