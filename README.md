# TP2- Jeux de mots / Synthèse et analyse spectrale d’une gamme de musique

Réalisé par:
Sara NHAILA (Filière: BigData Analytics)

Encadré par:

    Mr Alae Ammour

Objectifs:

    Comprendre comment manipuler un signal audio avec Matlab, en effectuant certaines opérations classiques sur un fichier audio d’une phrase enregistrée via un smartphone.
    Comprendre la notion des sons purs à travers la synthèse et l’analyse spectrale d’une gamme de musique.

<h1>Introduction:</h1>

L’analyse spectrale d’un signal consiste à trouver toutes les sinusoïdes qui contribuent significativement au signal : cela veut dire identifier les fréquences et les amplitudes des sinusoïdes associées. Un spectre de Fourier, ou spectre fréquentiel, est une représentation graphique permettant de visualiser ces deux grandeurs, où les fréquences sont en abscisses et les amplitudes en ordonnées.

Avec un signal périodique, le spectre se présente sous la forme de pics, situés au niveau de chaque fréquence intervenant dans le signal. Plus une fréquence contribue, plus le pic est haut, c'est-à-dire plus l’amplitude de la sinusoïde associée est forte.

# Jeux de mots
« phrase.wave » est un fichier audio enregistré à l’aide d’un smartphone, en prononçant lentement la phrase :
- « Rien ne sert de courir, il faut partir à point ».
- 1) Echantillonnage du signal en 4 morceaux après on change leur emplacements pour obtenir un nouveau signal .
- 2)chargement du fichier 'phrase.wav'
- 3)on le trace dans une figure avec la commande plot() qui prend comme argument le signal à visualiser
- 4)Pour délaté le signal, on divise la fréquence d’échantillonnage par 2 sound(y,Fs/2)on reçoit une version plus grave et moins rapide du son
-
#Script :


    clear all;
    close all;
    clc;
    fichier='phrase.wav'; %charger le fichier
    [x,fs]=audioread(fichier); %lire le fichier
    Te=1/fs;
    t=0:Te:(length(x)-1)*Te;
    %plot(t,x) %plot avec le temps
    %question3
    %sound(x,2*fs);compresion de son
    % sound(x,fs/2);delatation de son
    %question4:
    %plot(x); %tracer le signal en foction des indices du vecteur
    %question 5
    Riennesertde =x(1:82000); %indice correspond au rien ne sert de
    %sound(Riennesertde,22000); % pour ecouter juste rien ne sert de
    %question 6
    courir=x(82000:103300); %indice correspond au courir
    %sound(courir,22000); % pour ecouter courir
    ilfaut=x(103300:128900); %indice correspond au il faut
    %sound(ilfaut,22000); % pour ecouter il faut
    partirapoint=x(128900:171008); %indice correspond au partir a point
    %sound(partirapoint,22000); % pour ecouter partir a
    %question 7 écouter la phrase:Rien ne sert de partir apoint il faut courir, on
    % genere le vecteur suivant puis on l'écoute
    y=[Riennesertde partirapoint ilfaut courir];
    sound(y ,fs);
    
# Exécution :

Le signal avec le temps

![alt text](https://github.com/NhailaSara/TP2--Jeux-de-mots-Synth-se-et-analyse-spectrale-d-une-gamme-de-musique/blob/main/s1.png?raw=true)

Le signal sans temps pour récupérer les indices


![alt text](https://github.com/NhailaSara/TP2--Jeux-de-mots-Synth-se-et-analyse-spectrale-d-une-gamme-de-musique/blob/main/s2.png?raw=true)


# Exercice 2 : Synthèse et analyse spectrale d’une gamme de musique.

<h1>Synthèse d’une gamme de musique</h1>
<H3>1- Créez un programme qui permet de jouer une gamme de musique. La fréquence de chaque note est précisée dans le tableau ci-dessous. Chaque note aura une durée de 1s. La durée de la gamme sera donc de 8s. La fréquence d’échantillonnage fe sera fixée à 8192 Hz.</H3>


Les notes de musique produites par un piano peuvent être synthétisées approximativement numériquement. En effet, chaque note peut être considérée comme étant un son pur produit par un signal sinusoïdal. La fréquence de la note « La » est par exemple de 440 Hz.
# Le script :
    clear all
    close all
    clc
    fe=8192;%freuence d'd’échantillonnage
    Te=1/fe;
    t=0:Te:1;
    %decalarer les frequences de chaque note de la gamme
    DO1=262;
    RE=294;
    ME=330;
    Fa=349;
    SOL =392;
    la=440;
    Si=494;
    DO2=523;
    %generer un signal pour chaque note de gamme
    x=sin(2*pi*DO1*t);
    x1=sin(2*pi*RE*t);
    x2=sin(2*pi*ME*t);
    x3=sin(2*pi*Fa*t);
    x4=sin(2*pi*SOL*t);
    x5=sin(2*pi*la*t);
    x6=sin(2*pi*Si*t);
    x7=sin(2*pi*DO2*t);
    %combiner les notes pour obtenir la gamme musicale
    y=[x x1 x2 x3 x4 x5 x6 x7];
    sound(y ,fe);%ecouter la gamme
    %question 4 tracer la gamme en echelle lineaire
    N=length(y);
    f=(0:N-1)*(fe/N);
    A=fft(y);
    plot(f,abs(A));
    figure(2)
    %tracer la gamme en echelle decibel
    N=length(y);
    fshift = (-N/2:N/2-1)*(fe/N);
    DSP=abs(fft(y)).^2/N;
    % DSPr=DSP(1:N/2);
    plot(fshift,fftshift(mag2db(DSP)))

# Exécution :

![alt text](https://github.com/NhailaSara/TP2--Jeux-de-mots-Synth-se-et-analyse-spectrale-d-une-gamme-de-musique/blob/main/s3.png?raw=true)




