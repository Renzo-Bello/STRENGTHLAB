# STRENGTHLAB
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--font-sans)}
.app{padding:1.25rem 0}
.nav{display:flex;gap:8px;margin-bottom:1.25rem;flex-wrap:wrap}
.nav-btn{font-size:13px;padding:6px 14px;border-radius:99px;border:0.5px solid var(--color-border-secondary);background:transparent;color:var(--color-text-secondary);cursor:pointer;transition:all .15s}
.nav-btn.active{background:var(--color-text-primary);color:var(--color-background-primary);border-color:var(--color-text-primary)}
.search-wrap{margin-bottom:1rem;position:relative}
.search-wrap input{width:100%;padding-left:32px;font-size:14px}
.search-wrap .si{position:absolute;left:10px;top:50%;transform:translateY(-50%);font-size:16px;color:var(--color-text-secondary);pointer-events:none}
.ex-list{display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:8px;margin-bottom:1.25rem}
.ex-btn{text-align:left;padding:10px 12px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-tertiary);background:var(--color-background-primary);cursor:pointer;transition:all .15s}
.ex-btn:hover{border-color:var(--color-border-primary);background:var(--color-background-secondary)}
.ex-btn.active{border-color:var(--color-text-primary);background:var(--color-background-secondary)}
.ex-btn-name{font-size:13px;font-weight:500;color:var(--color-text-primary);line-height:1.3;margin-bottom:4px}
.ex-btn-group{font-size:11px;color:var(--color-text-secondary)}
.ficha{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);overflow:hidden}
.ficha-header{padding:1rem 1.25rem;border-bottom:0.5px solid var(--color-border-tertiary)}
.ficha-title{font-size:17px;font-weight:500;color:var(--color-text-primary);margin-bottom:3px}
.ficha-sub{font-size:12px;color:var(--color-text-secondary);text-transform:uppercase;letter-spacing:.04em}
.ficha-body{padding:1rem 1.25rem;display:grid;grid-template-columns:1fr 1fr;gap:1rem}
.ficha-section{grid-column:span 1}
.ficha-section.full{grid-column:span 2}
.section-title{font-size:11px;font-weight:500;text-transform:uppercase;letter-spacing:.06em;color:var(--color-text-secondary);margin-bottom:8px}
.step{display:flex;gap:8px;margin-bottom:7px;align-items:flex-start}
.step-n{width:20px;height:20px;border-radius:50%;background:var(--color-background-secondary);border:0.5px solid var(--color-border-secondary);font-size:11px;font-weight:500;color:var(--color-text-secondary);display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px}
.step-txt{font-size:13px;color:var(--color-text-primary);line-height:1.5}
.error-item{display:flex;gap:7px;margin-bottom:6px;align-items:flex-start}
.error-dot{width:6px;height:6px;border-radius:50%;background:#E24B4A;flex-shrink:0;margin-top:5px}
.error-txt{font-size:13px;color:var(--color-text-primary);line-height:1.5}
.tip-box{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:10px 12px;font-size:13px;color:var(--color-text-primary);line-height:1.5}
.muscles-wrap{display:flex;flex-wrap:wrap;gap:5px}
.badge{font-size:11px;padding:3px 9px;border-radius:99px}
.bp{background:#E6F1FB;color:#0C447C}
.bs{background:#F1EFE8;color:#5F5E5A}
.empty{text-align:center;padding:2.5rem 1rem;color:var(--color-text-secondary);font-size:14px}
@media(prefers-color-scheme:dark){.bp{background:#0C447C;color:#B5D4F4}.bs{background:#444441;color:#D3D1C7}}
@media(max-width:500px){.ficha-body{grid-template-columns:1fr}.ficha-section.full{grid-column:span 1}}
</style>

<div class="app">
<h2 class="sr-only">Guía de técnica de ejercicios de gimnasio</h2>
<div class="nav" id="nav"></div>
<div class="search-wrap">
  <i class="ti ti-search si" aria-hidden="true"></i>
  <input type="text" id="search" placeholder="Buscar ejercicio...">
</div>
<div class="ex-list" id="exList"></div>
<div id="fichaWrap"></div>
</div>

<script>
const DB = {
  empuje:[
    {name:"Press de banca con barra",group:"Pecho · horizontal",muscles:["Pectoral mayor","Tríceps","Deltoides anterior"],musclesS:["Serrato anterior","Core"],steps:["Túmbate en el banco con los pies apoyados en el suelo, espalda con arco natural y escápulas retraídas.","Agarra la barra con un ancho ligeramente mayor al de los hombros, muñecas rectas.","Baja la barra de forma controlada hasta tocar el pecho a la altura del pezón.","Empuja explosivamente hacia arriba manteniendo los codos a ~75° del cuerpo.","Extiende los brazos sin bloquear los codos al final del recorrido."],errors:["Rebotar la barra en el pecho en lugar de hacer una pausa controlada.","Despegar las caderas del banco para forzar más carga.","Codos demasiado abiertos a 90°, generando estrés en el hombro.","Muñecas dobladas hacia atrás al empujar."],tip:"Imagina que intentas partir la barra hacia afuera — esto activa más el pectoral y protege el hombro."},
    {name:"Press de banca con mancuernas",group:"Pecho · horizontal",muscles:["Pectoral mayor","Tríceps","Deltoides anterior"],musclesS:["Serrato anterior"],steps:["Siéntate al borde del banco con las mancuernas en los muslos, luego recuéstate llevándolas al pecho.","Pies en el suelo, espalda con arco natural, escápulas juntas y apoyadas en el banco.","Baja las mancuernas hasta que los codos queden ligeramente por debajo del nivel del banco.","Empuja hacia arriba y ligeramente hacia adentro, aproximando las mancuernas sin chocarlas.","Controla la bajada en 2-3 segundos."],errors:["Abrir demasiado los codos creando estrés en el hombro.","Perder la tensión en el pecho al cerrar las mancuernas arriba del todo.","Usar un rango de movimiento corto para manejar más carga."],tip:"Las mancuernas permiten un rango mayor que la barra — aprovéchalo bajando bien para maximizar el estiramiento."},
    {name:"Press inclinado con mancuernas",group:"Pecho superior · inclinado",muscles:["Pectoral mayor (porción clavicular)","Deltoides anterior","Tríceps"],musclesS:["Coracobraquial"],steps:["Ajusta el banco a 30-45°. Más ángulo activa más hombro que pecho.","Siéntate con las mancuernas en los muslos y recuéstate empujándolas.","Baja controlando hasta que los codos queden al nivel del banco.","Empuja hacia arriba y ligeramente hacia el centro.","Mantén las escápulas retraídas durante todo el movimiento."],errors:["Banco demasiado inclinado (>45°), que convierte el ejercicio en un press de hombros.","Perder la retracción escapular al subir.","Arquear excesivamente la espalda baja."],tip:"A 30° es el ángulo óptimo para la porción clavicular del pectoral sin sobrecargar el hombro."},
    {name:"Press Hammer Strength",group:"Pecho · máquina",muscles:["Pectoral mayor","Tríceps","Deltoides anterior"],musclesS:["Serrato anterior"],steps:["Ajusta el asiento para que las agarraderas queden a la altura del pecho medio.","Siéntate con la espalda completamente apoyada en el respaldo y el pecho abierto.","Empuja las palancas hacia adelante de forma controlada sin bloquear los codos.","Regresa lentamente sintiendo el estiramiento en el pecho.","Se puede trabajar un brazo a la vez para mayor concentración."],errors:["Despegar la espalda del respaldo para mover más carga.","Bloquear los codos al final del recorrido.","Agarre demasiado tenso que desvía el trabajo al hombro."],tip:"Al trabajar un brazo a la vez puedes rotar el torso levemente, aumentando el rango efectivo del pectoral."},
    {name:"Peck deck (mariposa)",group:"Pecho · aislamiento",muscles:["Pectoral mayor","Pectoral menor"],musclesS:["Deltoides anterior","Coracobraquial"],steps:["Ajusta el asiento para que los codos queden a la altura de los hombros al apoyarlos en los brazos de la máquina.","Mantén los codos ligeramente flexionados durante todo el movimiento — nunca completamente extendidos.","Junta los brazos al frente apretando el pecho en la posición de cierre.","Regresa lentamente abriendo bien para sentir el estiramiento.","Evita que los hombros suban hacia las orejas."],errors:["Codos completamente extendidos, lo que transfiere la tensión al hombro.","Rebotar en el punto de apertura máxima.","Hombros elevados durante el movimiento."],tip:"Aguanta 1 segundo en la posición cerrada apretando el pecho — esto maximiza la contracción muscular."},
    {name:"Fondos en paralelas",group:"Pecho / Tríceps · compound",muscles:["Pectoral mayor (porción esternal)","Tríceps"],musclesS:["Deltoides anterior","Serrato anterior"],steps:["Agarra las paralelas con los brazos extendidos y cuerpo ligeramente inclinado hacia adelante para más pecho.","Baja doblando los codos hasta que queden a 90° o hasta sentir estiramiento en el pecho.","Empuja explosivamente hacia arriba sin bloquear los codos al final.","Para más tríceps, mantén el torso erguido; para más pecho, inclínate hacia adelante."],errors:["Bajar demasiado, poniendo en riesgo el hombro.","Codos muy abiertos hacia los lados.","Balancear el cuerpo para generar impulso."],tip:"Inclinado = pecho. Erguido = tríceps. Controla el ángulo para elegir el énfasis."},
    {name:"Press militar con barra",group:"Hombros · vertical",muscles:["Deltoides anterior","Deltoides medio","Tríceps"],musclesS:["Trapecio superior","Core"],steps:["De pie o sentado, sujeta la barra con agarre a la anchura de los hombros.","Parte desde la clavícula con los codos ligeramente adelantados.","Empuja la barra directamente hacia arriba hasta la extensión completa.","Al bajar, mueve ligeramente la cabeza hacia atrás para dejar pasar la barra.","Mantén el core activo para proteger la zona lumbar."],errors:["Arquear excesivamente la espalda baja al empujar.","Llevar la barra hacia adelante en lugar de recta hacia arriba.","No activar el core, cargando la lumbar."],tip:"De pie activa más el core y el cuerpo completo — es más funcional que sentado."},
    {name:"Press militar con mancuernas",group:"Hombros · vertical",muscles:["Deltoides anterior","Deltoides medio","Tríceps"],musclesS:["Trapecio superior","Estabilizadores del hombro"],steps:["Sentado, comienza con las mancuernas a la altura de los hombros, palmas hacia adelante.","Empuja hacia arriba convergiendo levemente las mancuernas sin chocarlas en la parte alta.","Baja de forma controlada hasta que los codos queden ligeramente por debajo del hombro.","Mantén el abdomen tenso y la espalda apoyada en el respaldo."],errors:["Bajar los codos demasiado, sobrecargando el manguito rotador.","Arquear la espalda baja al empujar peso pesado.","Cabeza proyectada hacia adelante."],tip:"El mayor rango respecto a la barra y el trabajo unilateral te permiten detectar y corregir desequilibrios."},
    {name:"Elevaciones laterales",group:"Hombros · aislamiento",muscles:["Deltoides medio","Supraespinoso"],musclesS:["Deltoides anterior","Trapecio medio"],steps:["De pie, mancuernas a los costados con una leve flexión de codo (~15°).","Eleva los brazos lateralmente hasta la altura del hombro, no más arriba.","En la posición alta, el meñique debe estar ligeramente más alto que el pulgar (como verter agua).","Baja de forma muy controlada en 3 segundos — la bajada es tan importante como la subida."],errors:["Subir las mancuernas por encima del hombro, activando el trapecio en exceso.","Balancear el cuerpo para generar impulso.","Codos demasiado flexionados, reduciendo el torque en el deltoides."],tip:"Usa menos peso del que crees necesitar. El deltoides medio es pequeño y se fatiga rápido. La bajada controlada es donde más crece."},
    {name:"Extensión de tríceps en polea",group:"Tríceps · aislamiento",muscles:["Tríceps (cabeza lateral)","Tríceps (cabeza medial)","Tríceps (cabeza larga)"],musclesS:["Anconeo"],steps:["De pie frente a la polea alta, agarra la cuerda o barra con los codos pegados al cuerpo.","Flexiona levemente las rodillas y lleva el torso ligeramente hacia adelante.","Empuja hacia abajo extendiendo los codos completamente.","Con la cuerda, separa las manos al final para mayor activación de la cabeza lateral.","Regresa lentamente sin que los codos se muevan."],errors:["Separar los codos del cuerpo, convirtiendo el movimiento en un press.","No llegar a la extensión completa del codo.","Usar el peso del cuerpo para empujar en lugar del tríceps."],tip:"Con cuerda, abre las manos al final como si rompieras algo — activa más las tres cabezas del tríceps."}
  ],
  jalon:[
    {name:"Dominadas",group:"Espalda · jalón vertical",muscles:["Dorsal ancho","Redondo mayor"],musclesS:["Bíceps braquial","Romboides","Trapecio inferior","Core"],steps:["Agarra la barra con las manos a un ancho mayor que los hombros, palmas hacia afuera.","Parte de la posición colgante con los brazos completamente extendidos y el core activo.","Inicia el movimiento deprimiendo y retrayendo las escápulas antes de doblar los codos.","Jala hasta que la barbilla supere la barra, llevando los codos hacia abajo y atrás.","Baja de forma completamente controlada hasta la extensión total."],errors:["Usar el impulso del cuerpo en lugar de controlar el movimiento.","No bajar hasta la extensión completa — pierde el estiramiento del dorsal.","Encoger los hombros al final del tirón.","Cabeza hacia adelante para intentar alcanzar la barra."],tip:"Piensa en llevar los codos al bolsillo del pantalón — esto activa el dorsal mucho más que pensar en doblar los brazos."},
    {name:"Jalón al pecho",group:"Espalda · jalón vertical · polea",muscles:["Dorsal ancho","Redondo mayor"],musclesS:["Bíceps braquial","Trapecio inferior","Romboides","Infraespinoso"],steps:["Siéntate con los muslos bien sujetos bajo el rodillo, agarre prono ligeramente más ancho que los hombros.","Inclínate ligeramente hacia atrás (~15°) y comienza jalando deprimiendo las escápulas.","Jala la barra hacia la parte superior del pecho llevando los codos hacia abajo y atrás.","Aprieta el dorsal en la posición baja y regresa de forma controlada a la extensión completa."],errors:["Inclinar demasiado el torso hacia atrás, convirtiéndolo en un remo.","No llegar a la extensión completa arriba.","Jalar con los brazos sin iniciar el movimiento desde los hombros.","Codos que se abren hacia afuera al jalear."],tip:"Imagina que tienes naranjas bajo las axilas y las estás apretando — esto activa el dorsal desde el inicio."},
    {name:"Jalón unilateral",group:"Espalda · jalón un brazo",muscles:["Dorsal ancho","Redondo mayor"],musclesS:["Bíceps braquial","Romboides","Serrato anterior"],steps:["Siéntate ligeramente ladeado hacia la polea de trabajo.","Agarra con una mano y extiende el brazo completamente arriba.","Jala hacia abajo y hacia la cadera contraria, rotando levemente el torso.","Aprieta el dorsal al final del recorrido antes de regresar.","Mantén el hombro del lado libre hacia abajo y atrás."],errors:["No rotar el torso, perdiendo el mayor rango de movimiento que ofrece este ejercicio.","Usar impulso del cuerpo para manejar más peso.","Codo que se cierra demasiado hacia el cuerpo sin recorrido descendente."],tip:"La rotación del torso es la ventaja clave de este ejercicio — aprovéchala para un mayor estiramiento del dorsal."},
    {name:"Remo unilateral con mancuerna",group:"Espalda · remo horizontal",muscles:["Dorsal ancho","Romboides","Redondo mayor"],musclesS:["Trapecio medio e inferior","Bíceps braquial","Erectores espinales"],steps:["Apoya la rodilla y la mano del mismo lado en un banco para estabilizar la espalda plana.","La mancuerna cuelga con el brazo extendido hacia el suelo, hombro relajado.","Jala la mancuerna hacia la cadera (no hacia el hombro) llevando el codo hacia atrás.","Aprieta el dorsal y los romboides en la posición alta.","Baja completamente, dejando que el hombro se estire al final."],errors:["Jalar hacia el hombro en lugar de hacia la cadera — activa más bíceps que dorsal.","Rotar excesivamente el torso para mover más peso.","No dejar que el hombro se estire al final del recorrido."],tip:"Al final de cada rep, deja que el hombro caiga completamente — este estiramiento activo del dorsal es muy eficaz para el crecimiento."},
    {name:"Remo en polea baja",group:"Espalda · remo horizontal · polea",muscles:["Dorsal ancho","Romboides","Redondo mayor"],musclesS:["Trapecio medio","Bíceps braquial","Erectores espinales"],steps:["Siéntate con los pies en los apoyos, rodillas ligeramente flexionadas, espalda recta.","Extiende los brazos completamente hacia la polea para iniciar con estiramiento.","Jala el agarre hacia el abdomen bajo, llevando los codos hacia atrás.","Aprieta la espalda media al final antes de regresar controladamente.","Evita balancear el torso para generar impulso."],errors:["Redondear la espalda baja al jalear peso pesado.","Balancear el torso para generar momentum.","No estirar los brazos completamente al inicio de cada repetición."],tip:"Usa un agarre neutro (palmas enfrentadas) para maximizar la activación del dorsal y reducir la participación del bíceps."},
    {name:"Curl predicador (banco Scott)",group:"Bíceps · aislamiento",muscles:["Bíceps braquial (cabeza corta)","Braquial anterior"],musclesS:["Braquiorradial","Supinador largo"],steps:["Ajusta el banco para que las axilas descansen cómodamente en la parte superior del soporte.","Agarra la barra o mancuernas con supinación completa (palmas arriba).","Sube controlando sin que los codos se levanten del soporte.","Aprieta el bíceps en la posición alta con una supinación final del antebrazo.","Baja completamente — la extensión total es clave en este ejercicio."],errors:["No bajar completamente, perdiendo el estiramiento del bíceps.","Levantar los codos del soporte para ayudar en la subida.","Usar impulso del torso."],tip:"La extensión completa al bajar es lo que hace especial este ejercicio — muchos lo hacen a medio recorrido y pierden su mayor ventaja."},
    {name:"Curl en banco inclinado",group:"Bíceps · estiramiento",muscles:["Bíceps braquial (cabeza larga)","Braquial anterior"],musclesS:["Braquiorradial","Deltoides anterior"],steps:["Ajusta el banco a 45-60°. A mayor inclinación, mayor estiramiento de la cabeza larga.","Siéntate recostado, brazos colgando libremente hacia atrás.","Sube las mancuernas supinando el antebrazo al llegar arriba.","Aprieta el bíceps en la posición alta.","Baja lentamente dejando que los brazos cuelguen completamente."],errors:["Despegar los hombros del banco para ayudar en la subida.","No dejar colgar los brazos al bajar — si los sostienes, pierdes el estiramiento.","Bajar demasiado rápido perdiendo el control excéntrico."],tip:"El banco inclinado pone el hombro en extensión, estirando la cabeza larga — esto es lo que genera el pico del bíceps con el tiempo."},
    {name:"Curl martillo",group:"Bíceps / Braquial · agarre neutro",muscles:["Braquial anterior","Braquiorradial"],musclesS:["Bíceps braquial","Supinador largo","Extensor radial"],steps:["De pie, mancuernas a los costados con agarre neutro (palmas enfrentadas entre sí).","Sube alternando o simultáneamente sin girar el antebrazo — el pulgar siempre apunta arriba.","Lleva la mancuerna hacia el hombro del mismo lado.","Aprieta en la posición alta y baja controladamente.","Mantén los codos pegados al cuerpo durante todo el recorrido."],errors:["Rotar el antebrazo supinando — eso lo convierte en un curl normal.","Balancear el cuerpo para subir más peso.","Codos que se desplazan hacia adelante al subir."],tip:"El curl martillo trabaja principalmente el braquial, que está debajo del bíceps. Desarrollarlo empuja el bíceps hacia afuera, dando más grosor al brazo."}
  ],
  pierna:[
    {name:"Sentadilla libre con barra",group:"Cuádriceps / Glúteo · compound",muscles:["Cuádriceps","Glúteo mayor"],musclesS:["Isquiotibiales","Aductores","Core y erectores"],steps:["Barra apoyada en los trapecios (barra alta) o en los deltoides posteriores (barra baja). Core activo.","Pies a la anchura de los hombros o ligeramente más, punteras ligeramente abiertas.","Inicia el descenso empujando las caderas hacia atrás y abajo simultáneamente.","Baja hasta que los muslos queden paralelos al suelo o más abajo si la movilidad lo permite.","Sube empujando el suelo, manteniendo el torso erguido y las rodillas alineadas con los pies."],errors:["Rodillas que colapsan hacia adentro (valgo) al subir.","Redondear la espalda baja al llegar al punto más bajo.","Talones que se levantan — indica falta de movilidad de tobillo.","Torso que cae excesivamente hacia adelante."],tip:"Barra alta = más cuádriceps. Barra baja = más glúteo e isquios. Elige según tu objetivo."},
    {name:"Hack squat",group:"Cuádriceps · máquina guiada",muscles:["Cuádriceps","Glúteo mayor"],musclesS:["Isquiotibiales","Aductores","Gemelos"],steps:["Sube a la plataforma, espalda y glúteos completamente apoyados en el respaldo.","Pies a la anchura de los hombros, punteras ligeramente abiertas.","Libera los seguros y baja flexionando las rodillas de forma controlada.","Baja hasta 90° o más si la movilidad lo permite, sin que la zona lumbar se despegue.","Empuja la plataforma hacia arriba sin bloquear las rodillas al final."],errors:["Despegar la zona lumbar del respaldo al bajar — riesgo alto de lesión.","Bloquear las rodillas al extender arriba.","Pies demasiado juntos, generando estrés patelar."],tip:"Pies altos en la plataforma = más glúteo e isquios. Pies bajos = más énfasis en cuádriceps."},
    {name:"Prensa de piernas",group:"Cuádriceps · máquina",muscles:["Cuádriceps","Glúteo mayor"],musclesS:["Isquiotibiales","Aductores","Gemelos"],steps:["Siéntate con la espalda completamente apoyada, zona lumbar en contacto con el respaldo.","Pies a la anchura de los hombros en el centro de la plataforma.","Libera los seguros y baja la plataforma hasta que las rodillas formen 90°.","Empuja la plataforma hacia arriba sin bloquear las rodillas.","No permitas que las rodillas colapsen hacia adentro durante el empuje."],errors:["Levantar la zona lumbar del respaldo — riesgo serio de hernia.","Bajar demasiado doblando excesivamente la columna.","Bloquear las rodillas al extender.","Pies demasiado bajos, sobrecargando la rodilla."],tip:"Pies altos y separados = más glúteo. Pies bajos y juntos = más cuádriceps. Nunca bloquees las rodillas."},
    {name:"Extensión de cuádriceps",group:"Cuádriceps · aislamiento",muscles:["Recto femoral","Vasto lateral","Vasto medial","Vasto intermedio"],musclesS:[],steps:["Ajusta el asiento para que las rodillas queden alineadas con el eje de rotación de la máquina.","Ajusta el rodillo para que quede sobre el tobillo (no en el pie).","Extiende las piernas completamente, apretando el cuádriceps en la posición alta.","Aguanta 1 segundo arriba y baja en 3 segundos de forma controlada.","Evita usar impulso al subir."],errors:["No llegar a la extensión completa, perdiendo la contracción máxima del recto femoral.","Bajar demasiado rápido sin control excéntrico.","Rodillo mal colocado que genera estrés en el tobillo."],tip:"Un estudio reciente muestra que hacer este ejercicio con la cadera en extensión (recostado) activa más el recto femoral que de sentado."},
    {name:"Sentadilla pendular",group:"Cuádriceps / Glúteo · máquina",muscles:["Cuádriceps","Glúteo mayor"],musclesS:["Isquiotibiales","Aductores","Core"],steps:["Apoya los hombros en los acolchados y los pies en la plataforma.","Desengrana el seguro y permite que la máquina baje en su arco natural.","Baja hasta que los muslos queden paralelos o más, controlando el movimiento.","Empuja hacia arriba siguiendo la trayectoria del arco sin bloquear las rodillas.","Mantén la espalda apoyada en todo momento."],errors:["Bloquear las rodillas al extender.","Redondear la zona lumbar al llegar a la posición baja.","Pies demasiado altos en la plataforma que generan estrés lumbar."],tip:"La trayectoria en arco de la máquina permite bajar más profundo que la sentadilla libre con menor estrés en la columna."},
    {name:"Peso muerto rumano",group:"Isquiotibiales / Glúteo · hip hinge",muscles:["Isquiotibiales","Glúteo mayor"],musclesS:["Erectores espinales","Aductores","Core","Gemelos"],steps:["De pie, barra o mancuernas frente al cuerpo, agarre prono a la anchura de los hombros.","Flexiona levemente las rodillas y mantén esa flexión constante — no es una sentadilla.","Baja el peso deslizándolo por las piernas empujando las caderas hacia atrás.","Siente el estiramiento en los isquiotibiales al bajar — es la señal de rango correcto.","Sube empujando las caderas hacia adelante y apretando el glúteo al llegar arriba."],errors:["Doblar las rodillas en exceso, convirtiéndolo en sentadilla.","Redondear la espalda baja — el mayor riesgo de este ejercicio.","Bajar sin sentir el estiramiento en los isquios — indica que la espalda está redondeando.","Peso demasiado pesado que rompe la postura."],tip:"Si no sientes el estiramiento en los isquios al bajar, la carga es excesiva o la técnica está fallando. Reduce peso y prioriza la sensación muscular."},
    {name:"Sentadilla búlgara",group:"Cuádriceps / Glúteo · unilateral",muscles:["Cuádriceps","Glúteo mayor"],musclesS:["Isquiotibiales","Aductores","Core y estabilizadores"],steps:["Apoya el empeine del pie trasero en un banco a altura de rodilla.","El pie delantero debe estar suficientemente adelantado para que la rodilla no supere los dedos al bajar.","Baja doblando la rodilla delantera hasta que el muslo quede paralelo al suelo.","La rodilla trasera baja hacia el suelo de forma controlada.","Empuja a través del talón delantero para subir."],errors:["Pie delantero demasiado cerca del banco, forzando la rodilla delantera hacia adelante.","Torso que cae excesivamente hacia adelante.","Rodilla delantera que colapsa hacia adentro al subir.","Apoyar la punta del pie trasero en lugar del empeine."],tip:"Pie más adelantado = más glúteo. Pie más cercano al banco = más cuádriceps. Prueba ambas posiciones y elige según tu objetivo."},
    {name:"Curl de pierna sentado",group:"Isquiotibiales · aislamiento",muscles:["Bíceps femoral","Semitendinoso","Semimembranoso"],musclesS:["Gemelos (cabeza medial)","Poplíteo"],steps:["Ajusta el respaldo para que las rodillas queden en el borde del asiento.","Ajusta el rodillo para que quede sobre los tobillos.","Flexiona las rodillas jalando el rodillo hacia abajo y atrás.","Aprieta los isquiotibiales en la posición de máxima flexión.","Regresa de forma controlada sin dejar que el peso caiga."],errors:["Levantar las caderas del asiento al flexionar — reduce la activación.","No llegar a la flexión completa por usar demasiado peso.","Regresar demasiado rápido, perdiendo el control excéntrico."],tip:"La posición sentada mantiene la cadera flexionada, lo que pone los isquios en mayor estiramiento que el curl tumbado — mayor activación."},
    {name:"Abductor en máquina",group:"Glúteo medio · aislamiento",muscles:["Glúteo medio","Glúteo menor"],musclesS:["Tensor de la fascia lata","Glúteo mayor (porción superior)"],steps:["Siéntate con la espalda apoyada y las almohadillas en la cara externa de las rodillas.","Separa las piernas hacia afuera de forma controlada.","Aprieta el glúteo medio en la posición abierta.","Regresa lentamente sin dejar que las almohadillas choquen."],errors:["Inclinar el torso hacia adelante para ayudar en el movimiento.","Usar impulso en lugar de control muscular.","No llegar al rango completo de apertura."],tip:"Para mayor activación del glúteo medio, inclina levemente el torso hacia adelante — cambia el ángulo de trabajo sobre el músculo."},
    {name:"Aductor en máquina",group:"Muslo interno · aislamiento",muscles:["Aductor largo","Aductor mayor","Aductor corto"],musclesS:["Grácil","Pectíneo"],steps:["Siéntate con la espalda apoyada y las almohadillas en la cara interna de las rodillas.","Junta las piernas de forma controlada apretando los aductores.","Aguanta 1 segundo en la posición cerrada.","Regresa lentamente abriendo bien para sentir el estiramiento."],errors:["Rango de movimiento corto que no aprovecha el estiramiento de los aductores.","Usar demasiado peso y perder el control.","No mantener la espalda apoyada en todo momento."],tip:"Los aductores también contribuyen a la extensión de cadera — son más importantes de lo que parece para la sentadilla y el peso muerto."},
    {name:"Gemelos en máquina",group:"Pantorrilla · aislamiento",muscles:["Gastrocnemio (cabeza medial y lateral)","Sóleo"],musclesS:["Tibial posterior","Flexor largo de los dedos"],steps:["Coloca la parte anterior del pie en el borde de la plataforma, talón colgando.","Baja el talón completamente para un estiramiento máximo del gastrocnemio.","Sube en puntillas lo más alto posible y aprieta los gemelos.","Aguanta 1 segundo arriba antes de bajar.","Controla la bajada en 2-3 segundos."],errors:["Rango corto — ni bajo ni sube completamente.","Usar rebote en la posición baja en lugar de estiramiento controlado.","Rodillas dobladas (activa más el sóleo que el gastrocnemio)."],tip:"De pie (rodillas extendidas) = más gastrocnemio. Sentado (rodillas flexionadas) = más sóleo. Trabaja ambas variantes para una pantorrilla completa."}
  ]
};

const catColors = {empuje:'#185FA5',jalon:'#534AB7',pierna:'#854F0B'};
const catNames = {empuje:'Empuje',jalon:'Jalón',pierna:'Pierna'};

let currentCat = 'empuje';
let currentEx = null;

function renderNav(){
  const nav = document.getElementById('nav');
  nav.innerHTML = '';
  ['empuje','jalon','pierna'].forEach(c=>{
    const b = document.createElement('button');
    b.className = 'nav-btn' + (c===currentCat?' active':'');
    b.textContent = catNames[c] + ' (' + DB[c].length + ')';
    b.onclick = ()=>{ currentCat=c; currentEx=null; renderAll(); };
    nav.appendChild(b);
  });
}

function renderList(filter){
  const list = document.getElementById('exList');
  list.innerHTML = '';
  const items = filter
    ? Object.values(DB).flat().filter(e=>e.name.toLowerCase().includes(filter.toLowerCase()))
    : DB[currentCat];
  if(!items.length){
    list.innerHTML = '<div class="empty">No se encontraron ejercicios</div>';
    return;
  }
  items.forEach((ex,i)=>{
    const btn = document.createElement('button');
    btn.className = 'ex-btn' + (ex===currentEx?' active':'');
    btn.innerHTML = '<div class="ex-btn-name">'+ex.name+'</div><div class="ex-btn-group">'+ex.group+'</div>';
    btn.onclick = ()=>{ currentEx=ex; renderFicha(); renderList(filter); };
    list.appendChild(btn);
  });
}

function renderFicha(){
  const wrap = document.getElementById('fichaWrap');
  if(!currentEx){ wrap.innerHTML=''; return; }
  const ex = currentEx;
  const steps = ex.steps.map((s,i)=>`<div class="step"><div class="step-n">${i+1}</div><div class="step-txt">${s}</div></div>`).join('');
  const errors = ex.errors.map(e=>`<div class="error-item"><div class="error-dot"></div><div class="error-txt">${e}</div></div>`).join('');
  const musPri = ex.muscles.map(m=>`<span class="badge bp">${m}</span>`).join('');
  const musSec = ex.musclesS.map(m=>`<span class="badge bs">${m}</span>`).join('');
  wrap.innerHTML = `
  <div class="ficha">
    <div class="ficha-header">
      <div class="ficha-title">${ex.name}</div>
      <div class="ficha-sub">${ex.group}</div>
    </div>
    <div class="ficha-body">
      <div class="ficha-section full">
        <div class="section-title">Músculos</div>
        <div class="muscles-wrap">${musPri}${musSec}</div>
      </div>
      <div class="ficha-section">
        <div class="section-title">Técnica paso a paso</div>
        ${steps}
      </div>
      <div class="ficha-section">
        <div class="section-title">Errores comunes</div>
        ${errors}
        <div class="section-title" style="margin-top:1rem">Tip clave</div>
        <div class="tip-box">${ex.tip}</div>
      </div>
    </div>
  </div>`;
  wrap.scrollIntoView({behavior:'smooth',block:'nearest'});
}

function renderAll(filter){
  renderNav();
  renderList(filter);
  renderFicha();
}

document.getElementById('search').addEventListener('input', function(){
  const v = this.value.trim();
  if(v) renderList(v);
  else renderList();
});

renderAll();
</script>
