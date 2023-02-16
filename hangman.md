<style>
body {
    background: #DADFF7;
}
.letter {
  height: 25px;
  width: 25px;
  display: inline-block;
  text-align: center;
  min-width:30px;
  border: solid 2px black;
  color: black;
  background-color: #5A7D7C;
  padding:2px;
  font-size: 22px;
  margin: 0px 2.5px 0px 2.5px;
  cursor: pointer;
}

.divider {
  margin-bottom: 20px;
}
.used {
  cursor: not-allowed;
  background-color: #232C33;
  color: #DADFF7;
}

#left, #right {
  padding: 25px;
}

#characters {
  text-align: center;
}

#guesses {
  text-align: center;
  color: black;
  font-size: 2em;
}

.stacked {
  position: absolute;
  background: white;
 // margin: 25px;
  //float: left;
}

.top {
  z-index: 1;
}

#letters { display: block; clear: both; text-align: center;}
#resetGame {
  text-align: center;
  width: 100%;
  padding: 10px;
  margin-top: 20px;
  background: black;
  color: white;
}

#left {
}

#right {
  margin: 0 auto;
  width: 25%;
}

#hangman {
  top: 30px;
  position: absolute;
}
</style>

<div id="game wrapper">
  <div id="right">
    <div id="letters"></div>
    <div id="guesses"></div>
    <div id="characters"></div>
    <div id="newGame">
    <button id="resetGame">New Game</button>
  </div>
  </div>
  <div id="left">
    <div id="hangman">
    </div>
<script>
class Hangman {
  constructor(difficulty, players) {
    this.difficulty = difficulty
    this.players    = players
    this.guessed    = []
    this.strikes    = 0
    // SHOULD DETERMINE BY DIFFICULTY
    this.maxStrikes = 6
  }
  reset () {
    this.guessed = []
    this.strikes = 0
    this.setWord()
    $('.letter').removeClass('used')
    for(let i = 1; i <= 6; i++) {
      $(`#hangman-${i}`).removeClass('top')
      }
  }
  checkGameOver() {
    if(this.strikes >= this.maxStrikes) {
      // do gameover stuff
      alert('Game Over')
      $('#letters').html(
        this.word.split('').map(l =>
                                `<span class="letter">${l.toUpperCase()}</span>`
      ).join('')
      )
    }
  }
  letterCheck(letter) {
    if(this.guessed.includes(letter)) {
      alert('You already guessed: ' + letter)
    } else {
      if(!this.word.split('').includes(letter)) {
        this.strikes += 1
       // $('#hangman').html(`<img src="https://justinbess.com/wp-content/uploads/2018/04/${this.strikes}.png"/>`)
        $(`#hangman-${this.strikes}`).addClass('top')
      }
      this.guessed.push(letter)
    }
    this.update()
  }
  letterClick(letter, el) {
    $(el).addClass('used');
    this.letterCheck(letter)
  }
  createLetters() {
    let self = this;
    let range = {
      init: 65,
      end: 90,
      divider: 9
    }
    let div = document.getElementById('characters');
    for(var i = range.init; i <= range.end; i++) {
      if((i - 65) % range.divider == 0) {
        let divider = document.createElement('div');
        divider.classList.add('divider');
        div.appendChild(divider);
      }
      let letter = String.fromCharCode(i);
      let span = document.createElement('span');
      span.classList.add('letter');
      span.innerText = letter;
      div.appendChild(span);
      span.addEventListener('click', () => {
        self.letterClick(letter, span);
      });
    }
  }
  setWord () {
    let words = ['tropical', 'assigned', 'coordinated']
    let num = Math.floor(Math.random() * 3)
    this.word = words[num].split('').map(l => l.toUpperCase()).join('')
    this.update()
  }
  transformWord () {
    let transform = []
    let letters = this.word.split('')
    letters.map(l => {
      this.guessed.includes(l.toUpperCase()) ? 
        transform.push(`<span class="letter">${l.toUpperCase()}</span>`) :
        transform.push(`<span class="letter"></span>`)
    })
    return transform.join('')
  }
  update () {
    $('#guesses').html(`Wrong Guesses: ${this.strikes}/${this.maxStrikes}` )
    $('#letters').html(this.transformWord(this.word))
    this.checkGameOver()
  }
  createImages () {
    let images = []
    for(let i = 0; i <= 6; i++) {
      images.push(`<img class="stacked" id="hangman-${i}" src="https://justinbess.com/wp-content/uploads/2018/04/${i}.png"/>`)
    }
    $('#hangman').html(images.join(''))
    $('#hangman-0').addClass('top')
  }
  initialize () {
    this.createImages()
    this.createLetters()
    this.setWord()
  }
}
let game = new Hangman('easy', 1);
game.initialize()
$('#resetGame').click(function() {
  game.reset()
})
</script>
  </div>
</div>