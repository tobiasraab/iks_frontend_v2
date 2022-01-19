<template>
  <div id="screen">
    <TheBackground
      :id="'background_template'"
      :heading="background.heading"
      :text="background.text"
      :imagesrc="background.imageSrc"
    />
    <TheInfoSide
      :data="infoSide"
      :steps="steps"
    />
  </div>
</template>

<script>
import TheInfoSide from '~/components/TheInfoSide.vue'
import TheBackground from '~/components/TheBackground.vue'

export default {
  name: 'IndexPage',
  components: {
    TheInfoSide,
    TheBackground
  },
  data () {
    return {
      background: {
        heading: null,
        text: null,
        imageSrc: null
      },
      socket: undefined,
      allPassive: undefined,
      focusState: undefined,
      infoSide: {
        heading1: 'Test Überschrift1',
        text1: 'Test Text 1',

        heading2: 'Test Überschrift2',
        text2: 'Test Text 3',
        topic: 'Anleitung',
        builder: 'Sei der Baumeister des Ulmer Münsters! \n\n So funktioniert´s: ...',
        time: null,
        info: null,
        imgtitle: null,
        imgsrc: null,
        titleBuilder: 'Info'
      },
      steps: [
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Westturm Dach',
          time: '1890',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 0
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Ostturm Süd',
          time: '1885',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 2
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Ostturm Nord',
          time: '1880',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 2
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Baustop und Restaurierung',
          time: '1543',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 400
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Seitenschiff Nr.5',
          time: '1507',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 40
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Seitenschiff Nr.4',
          time: '1502',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 2
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'provisorisches Turmdach',
          time: '1492',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 8
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Westturm',
          time: '1477',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 14
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Dach',
          time: '1475',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 0
        },
        {
          text1: 'test text1',
          heading2: 'Baumeister',
          text2: 'test text 2',
          name: 'Seiten- und Mittelschiff',
          time: '1452',
          state: 'passive',
          backgroundHeading: 'Header',
          backgroundInfoText: 'toller text',
          backgroundInfoImg: require('~/assets/images/muenster-bauplan.jpg'),
          margin: 24
        },
        {
          text1: 'Der Bau der Kirche wurde 1377 von Heinrich II. Parler im Osten mit dem Chor und den Unterbauten begonnen.',
          heading2: 'Baumeister',
          text2: 'Heinrich ll. Parler (1377-1383)\nMichael lll. Parler (1383-1392)\nFamilie Ensinger & Kun (1392-1477)',
          name: 'Unterbau',
          time: '1377',
          state: 'passive',
          backgroundHeading: 'Markus lll. Parler',
          backgroundInfoText: 'Das Baumeisterbild am Chorgesims im Winkel zwischen Chor und Südturm im Ulmer Münster zeigt vermutlich Michael Parler. Bis 1387 leitete er den Münsterbau. Unter seiner Regie wurde u.a. mit dem Langhaus begonnen und „der Chor mit dem ersten Kranzgesims abgeschlossen“ und provisorisch abgedeckt. Damit war die Möglichkeit geschaffen, einen Altar aufzustellen und Gottesdienste zu feiern.',
          backgroundInfoImg: require('~/assets/images/markus-parler.png'),
          margin: 76
        },
        {
          text1: '30.6.1377 wurde der Grundstein für die neue Kirche gelegt. Die Ulmer wollten eine Kirche, die dem Ansehen der politisch mächtigen und wirtschaftlich wohlhabenden Reichsstadt angemessen war. Dazu waren die Bürger bereit sich fina-ziell zu beteiligen. Es sollte eine Bürgerkirche werden, also ohne die Unterstützung eines Bischofs oder Fürsten zu finanziert werden.',
          heading2: 'Baumeister',
          text2: 'Heinrich ll. Parler (1377-1383)',
          name: 'Grundsteinlegung',
          time: '1377',
          state: 'passive',
          backgroundHeading: 'Grundsteinrelief',
          backgroundInfoText: 'Die Gedenktafel zeigt Altbürgermeister Lutz Kraft und seine Frau Elisabeth Ehinger. Beide legen einer Person, bei der es sich um den ersten Münsterbaumeister Heinrich II. Parler handeln dürfte, mit dem Modell einer Hallenkirche symbolisch die ganze Baulast auf die Schultern. Darüber eine Inschrift mit Jahrestag und Stunde der Grundsteinlegung.',
          backgroundInfoImg: require('~/assets/images/Ulm-Muenster-Gruendungsrelief.jpg'),
          margin: 0
        }
      ]
    }
  },
  watch: {
    steps: {
      deep: true,
      handler () {
        console.warn('change')
        // update lists
        this.focusState = false
        // search focused theme
        for (let i = 0; i < this.steps.length; i++) {
          if (this.steps[i].state === 'focus') {
            // change data for the info side
            this.infoSide = {
              topic: this.steps[i].name,
              time: this.steps[i].time,
              imgtitle: this.steps[i].imgtitle,
              imgsrc: this.steps[i].imgsrc
            }
            this.background = {
              heading: this.steps[i].backgroundHeading,
              text: this.steps[i].backgroundInfoText,
              imageSrc: this.steps[i].backgroundInfoImg
            }
            console.log(this.background)
            this.focusState = true
          }
          if (!this.focusState) {
            this.infoSide = {
              topic: null,
              builder: null,
              time: null,
              info: null,
              imgtitle: null,
              imgsrc: null,
              titleBuilder: null
            }
            this.background = {
              heading: null,
              text: null,
              imageSrc: null
            }
          }
        }

        // default start state?
      }
    }
  },
  mounted () {
    // Connect Socket
    this.socket = this.$nuxtSocket({
    })
    this.socket
      .on('connect', () => {
        console.log('SERVER_CONNECTED')

        // update state of steps
        this.socket.on('data', (data) => {
          console.log('INCOMING: ', data)
          for (let i = 0; i < this.steps.length; i++) {
            this.steps[i].state = data[i]
          }
        })
      })
  }
}
</script>

<style>
@import "~/assets/fonts/fontFrutiger.css";

body {
  font-family: 'frutigermedium';
  margin: 0;
  padding: 0;
}

#screen{
  background-color: #000000;
  max-height: 100vh;
  display: block;
}

#background_template{
  position: absolute;
  width: 100vw;
  height: 100vh;
  background-color: #000000;
}
</style>
