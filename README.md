# js-pong
//variáveis da bolinha
let xBolinha = 100;
let yBolinha = 200;
let diametro = 22;
let raio = diametro / 2;

//variáveis do oponente
let xRaqueteOponente = 585;
let yRaqueteOponente = 150;

//velocidade da bolinha
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;

//variáveis da raquete
let xRaquete = 5;
let yRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 90;

let colidiu = false;

//placar do jogo
let meusPontos = 0;
let pontosOponente = 0;
let Deus;
let ponto;
let raquetada;
let trilha;

function preload() {
  Deus = loadImage("Deus.jpg");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
  trilha = loadSound("trilha.mp3");
  jk = loadSound("jk.mp3");
}


function setup() {
  createCanvas(600, 400);
  jk.loop();
}

function draw() {
    background(Deus);
    mostraBolinha();
    movimentaBolinha();
    verificaColisaoBorda();
    mostraRaquete(xRaquete, yRaquete);
    movimentaMinhaRaquete();
    verificaColisaoRaquete(xRaquete, yRaquete);
    verificaColisaoRaquete(xRaqueteOponente, yRaqueteOponente);
    mostraRaquete(xRaqueteOponente, yRaqueteOponente);
    movimentaRaqueteOponente();
    incluiPlacar();
    marcaPonto();
    bolinhaNaoFicaPresa();
}
function mostraBolinha() {
  circle(xBolinha, yBolinha, diametro);
}
function movimentaBolinha() {
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}

function verificaColisaoBorda() {
  if (xBolinha + raio > width || xBolinha - raio < 0) {
    velocidadeXBolinha *= -1;
  }
  if (yBolinha + raio > height || yBolinha - raio < 0) {
    velocidadeYBolinha *= -1;
  }
}

function mostraRaquete(x,y) {
    rect(x, y, raqueteComprimento, raqueteAltura);
}

function movimentaMinhaRaquete() {
  if(keyIsDown(UP_ARROW)) {
    yRaquete -= 10;
  }
  if(keyIsDown(DOWN_ARROW)) {
    yRaquete += 10;
  }
}

function verificaColisaoRaquete() {
  if (xBolinha - raio < xRaquete + raqueteComprimento && yBolinha - raio < yRaquete + raqueteAltura && yBolinha + raio > yRaquete) {
    velocidadeXBolinha *= -1;
  }
}

function verificaColisaoRaquete(x, y) {
    colidiu = collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
    if (colidiu){
        velocidadeXBolinha *= -1;
        raquetada.play()
  }
}

function movimentaRaqueteOponente() {
    velocidadeyOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
    yRaqueteOponente += velocidadeyOponente
}

function incluiPlacar() {
  textAlign(CENTER, CENTER);
  textSize(000);
  fill(color(000,000,0));
  rect(130, 14, 40, 20);
  fill(255);
  stroke("black");
  text(meusPontos, 150, 26);
  fill(color(000,000,0));
  rect(430, 14, 40, 20);
  fill(255);
  stroke("black");
  text(pontosOponente, 450, 26);
}

function marcaPonto() {
   if(xBolinha > 585) {
     meusPontos += 1;
     ponto.play();
   }
   if(xBolinha < 15) {
     pontosOponente += 1;
     ponto.play();
   }
 }

function bolinhaNaoFicaPresa(){
  if(xBolinha - raio < 0){
    xBolinha = 23;
  }
