<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dbacf9b1915612981d76059678e563e5",
  "translation_date": "2025-08-25T23:30:54+00:00",
  "source_file": "lessons/6-Other/22-DeepRL/README.md",
  "language_code": "sk"
}
-->
# Hlboké posilňovacie učenie

Posilňovacie učenie (RL) je považované za jeden zo základných paradigmov strojového učenia, vedľa učenia s učiteľom a učenia bez učiteľa. Zatiaľ čo pri učení s učiteľom sa spoliehame na dataset s známymi výsledkami, RL je založené na **učení sa prostredníctvom skúseností**. Napríklad, keď prvýkrát vidíme počítačovú hru, začneme ju hrať, aj keď nepoznáme pravidlá, a čoskoro dokážeme zlepšiť svoje schopnosti len procesom hrania a prispôsobovania svojho správania.

## [Kvíz pred prednáškou](https://ff-quizzes.netlify.app/en/ai/quiz/43)

Na vykonanie RL potrebujeme:

* **Prostredie** alebo **simulátor**, ktorý nastavuje pravidlá hry. Mali by sme byť schopní vykonávať experimenty v simulátore a pozorovať výsledky.
* **Funkciu odmeny**, ktorá naznačuje, ako úspešný bol náš experiment. V prípade učenia sa hrať počítačovú hru by odmenou bolo naše konečné skóre.

Na základe funkcie odmeny by sme mali byť schopní prispôsobiť svoje správanie a zlepšiť svoje schopnosti, aby sme nabudúce hrali lepšie. Hlavný rozdiel medzi inými typmi strojového učenia a RL je ten, že pri RL zvyčajne nevieme, či vyhráme alebo prehráme, až kým nedokončíme hru. Preto nemôžeme povedať, či je určitý krok sám o sebe dobrý alebo nie - odmenu dostaneme až na konci hry.

Počas RL zvyčajne vykonávame mnoho experimentov. Počas každého experimentu musíme vyvážiť medzi nasledovaním optimálnej stratégie, ktorú sme sa doteraz naučili (**využívanie**), a skúmaním nových možných stavov (**prieskum**).

## OpenAI Gym

Skvelým nástrojom pre RL je [OpenAI Gym](https://gym.openai.com/) - **simulačné prostredie**, ktoré dokáže simulovať mnoho rôznych prostredí, od hier Atari až po fyziku za vyvažovaním tyče. Je to jedno z najpopulárnejších simulačných prostredí na trénovanie algoritmov posilňovacieho učenia a je udržiavané [OpenAI](https://openai.com/).

> **Note**: Všetky dostupné prostredia z OpenAI Gym si môžete pozrieť [tu](https://gym.openai.com/envs/#classic_control).

## Vyvažovanie CartPole

Pravdepodobne ste už videli moderné vyvažovacie zariadenia, ako napríklad *Segway* alebo *Gyroskútre*. Dokážu automaticky vyvažovať tým, že upravujú svoje kolesá na základe signálu z akcelerometra alebo gyroskopu. V tejto sekcii sa naučíme, ako vyriešiť podobný problém - vyvažovanie tyče. Je to podobné situácii, keď cirkusový umelec potrebuje vyvážiť tyč na svojej ruke - ale toto vyvažovanie tyče sa deje iba v 1D.

Zjednodušená verzia vyvažovania je známa ako problém **CartPole**. Vo svete CartPole máme horizontálny posúvač, ktorý sa môže pohybovať doľava alebo doprava, a cieľom je vyvážiť vertikálnu tyč na vrchu posúvača, keď sa pohybuje.

<img alt="cartpole" src="images/cartpole.png" width="200"/>

Na vytvorenie a použitie tohto prostredia potrebujeme niekoľko riadkov kódu v Pythone:

```python
import gym
env = gym.make("CartPole-v1")

env.reset()
done = False
total_reward = 0
while not done:
   env.render()
   action = env.action_space.sample()
   observaton, reward, done, info = env.step(action)
   total_reward += reward

print(f"Total reward: {total_reward}")
```

Každé prostredie je možné pristupovať presne rovnakým spôsobom:
* `env.reset` spustí nový experiment
* `env.step` vykoná simulačný krok. Prijíma **akciu** z **akčného priestoru** a vracia **pozorovanie** (z pozorovacieho priestoru), ako aj odmenu a príznak ukončenia.

V príklade vyššie vykonávame náhodnú akciu pri každom kroku, čo je dôvod, prečo je život experimentu veľmi krátky:

![nevyvážené cartpole](../../../../../lessons/6-Other/22-DeepRL/images/cartpole-nobalance.gif)

Cieľom algoritmu RL je vytrénovať model - tzv. **politiku** π - ktorá bude vracať akciu v reakcii na daný stav. Politiku môžeme tiež považovať za pravdepodobnostnú, napr. pre akýkoľvek stav *s* a akciu *a* bude vracať pravdepodobnosť π(*a*|*s*), že by sme mali vykonať *a* v stave *s*.

## Algoritmus Policy Gradients

Najzjavnejší spôsob modelovania politiky je vytvorenie neurónovej siete, ktorá bude brať stavy ako vstup a vracať zodpovedajúce akcie (alebo skôr pravdepodobnosti všetkých akcií). V istom zmysle by to bolo podobné bežnej klasifikačnej úlohe, s hlavnou odlišnosťou - vopred nevieme, ktoré akcie by sme mali vykonať pri každom kroku.

Myšlienka je tu odhadnúť tieto pravdepodobnosti. Vytvoríme vektor **kumulatívnych odmien**, ktorý ukazuje našu celkovú odmenu pri každom kroku experimentu. Tiež aplikujeme **diskontovanie odmien** násobením skorších odmien nejakým koeficientom γ=0.99, aby sme znížili význam skorších odmien. Potom posilníme tie kroky pozdĺž experimentálnej cesty, ktoré prinášajú väčšie odmeny.

> Viac o algoritme Policy Gradient a jeho ukážku nájdete v [príkladovom notebooku](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb).

## Algoritmus Actor-Critic

Vylepšená verzia prístupu Policy Gradients sa nazýva **Actor-Critic**. Hlavná myšlienka za tým je, že neurónová sieť by mala byť trénovaná na návrat dvoch vecí:

* Politiku, ktorá určuje, akú akciu vykonať. Táto časť sa nazýva **actor**.
* Odhad celkovej odmeny, ktorú môžeme očakávať v tomto stave - táto časť sa nazýva **critic**.

V istom zmysle táto architektúra pripomína [GAN](../../4-ComputerVision/10-GANs/README.md), kde máme dve siete, ktoré sú trénované proti sebe. V modeli actor-critic navrhuje actor akciu, ktorú potrebujeme vykonať, a critic sa snaží byť kritický a odhadnúť výsledok. Naším cieľom je však trénovať tieto siete v súlade.

Keďže poznáme skutočné kumulatívne odmeny a výsledky, ktoré critic vracia počas experimentu, je relatívne jednoduché vytvoriť funkciu straty, ktorá minimalizuje rozdiel medzi nimi. To nám dáva **critic loss**. **Actor loss** môžeme vypočítať použitím rovnakého prístupu ako v algoritme Policy Gradient.

Po spustení jedného z týchto algoritmov môžeme očakávať, že naše CartPole sa bude správať takto:

![vyvážené cartpole](../../../../../lessons/6-Other/22-DeepRL/images/cartpole-balance.gif)

## ✍️ Cvičenia: Policy Gradients a Actor-Critic RL

Pokračujte vo svojom učení v nasledujúcich notebookoch:

* [RL v TensorFlow](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb)
* [RL v PyTorch](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-PyTorch.ipynb)

## Ďalšie úlohy RL

Posilňovacie učenie je dnes rýchlo rastúcou oblasťou výskumu. Niektoré zaujímavé príklady posilňovacieho učenia sú:

* Učenie počítača hrať **hry Atari**. Náročnou časťou tohto problému je, že nemáme jednoduchý stav reprezentovaný ako vektor, ale skôr snímku obrazovky - a musíme použiť CNN na konverziu obrazu obrazovky na vektor vlastností alebo na extrakciu informácií o odmene. Hry Atari sú dostupné v Gym.
* Učenie počítača hrať stolové hry, ako šach a Go. Nedávno boli programy na špičkovej úrovni, ako **Alpha Zero**, trénované od nuly dvoma agentmi, ktorí hrali proti sebe a zlepšovali sa pri každom kroku.
* V priemysle sa RL používa na vytváranie riadiacich systémov zo simulácie. Služba nazývaná [Bonsai](https://azure.microsoft.com/services/project-bonsai/?WT.mc_id=academic-77998-cacaste) je špeciálne navrhnutá na tento účel.

## Záver

Teraz sme sa naučili, ako trénovať agentov na dosiahnutie dobrých výsledkov len poskytnutím funkcie odmeny, ktorá definuje požadovaný stav hry, a umožnením inteligentného skúmania priestoru hľadania. Úspešne sme vyskúšali dva algoritmy a dosiahli dobrý výsledok v relatívne krátkom čase. Toto je však len začiatok vašej cesty do RL, a určite by ste mali zvážiť absolvovanie samostatného kurzu, ak chcete ísť hlbšie.

## 🚀 Výzva

Preskúmajte aplikácie uvedené v sekcii 'Ďalšie úlohy RL' a skúste implementovať jednu z nich!

## [Kvíz po prednáške](https://ff-quizzes.netlify.app/en/ai/quiz/44)

## Prehľad a samostatné štúdium

Viac o klasickom posilňovacom učení sa dozviete v našom [kurze Machine Learning for Beginners](https://github.com/microsoft/ML-For-Beginners/blob/main/8-Reinforcement/README.md).

Pozrite si [toto skvelé video](https://www.youtube.com/watch?v=qv6UVOQ0F44), ktoré hovorí o tom, ako sa počítač môže naučiť hrať Super Mario.

## Zadanie: [Vytrénujte Mountain Car](lab/README.md)

Vaším cieľom počas tohto zadania bude vytrénovať iné prostredie Gym - [Mountain Car](https://www.gymlibrary.ml/environments/classic_control/mountain_car/).

**Zrieknutie sa zodpovednosti**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nenesieme zodpovednosť za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.