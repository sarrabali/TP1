# TP1
cryptography
from collections import Counter
FrFrequence = {'a': 0.094, 'b': 0.01, 'c': 0.026, 'd': 0.034, 'e':0.159, 'f': 0.01, 'g': 0.01,
             'h': 0.008, 'i': 0.084, 'j': 0.009, 'k': 0, 'l': 0.053, 'm': 0.032, 'n': 0.072,
             'o': 0.051, 'p': 0.029, 'q': 0.011, 'r': 0.065, 's': 0.079, 't': 0.073, 'u': 0.062,
                   'v': 0.021, 'w': 0, 'x': 0.003, 'y': 0.002, 'z': 0.003}
Letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l',
           'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']
NumberLetters =  len(Letters)


def Lettre_cesar(letter, var):
    return chr((ord(letter) - var - 97) % 26 + 97)


def Cesar(sentence, var):
    return "".join(Lettre_cesar(letter, var) for letter in sentence)


def CalcDistance(text_length, counter, key):
    return sum([abs(counter.get(Lettre_cesar(letter, -key % 26), 0) * text_length - FrFrequence[letter])
                for letter in Letters]) / NumberLetters


def CesarFrequencyAttack(cipher_text, counter):
    distances = [CalcDistance(len(cipher_text), counter, key)
                 for key in range(NumberLetters)]
    return distances.index(min(distances))


text = "mobdksxczyebbksoxdzbodoxnboaeexvsfboaesdbksdonemynoocdexvsfbonozkccovomynoxocdzvecvozbylvowoodaesvocdzvecswzybdkxdketyebnresnocsxdoboccobkehwynovocodkehohsqoxmocsvkwowoodoceqqoboaeovkpsxnemynoodksdzbymroaesvcobksdlsoxdydqoxobokevsoenodboombsdaeovoczbyqbkwwoebccobksoxdlsoxdydsxedsvocmkbvocnsbomdoebcnozbytodcqoxobobksoxdvoczbyqbkwwockzkbdsbnocczomspsmkdsyxclkvsfobxocxyecxozyebbyxctkwkscxyecnolkbbkccobnemynomkbsvbozbocoxdovocnodksvcnocohsqoxmockexmobdksxxsfokemocnodksvcxozoefoxdzkcodbosqxybocyeklcoxdcsvcnysfoxdodbozbomscoczbomscobnocohsqoxmockexxsfokenonodksvaeszobwodkexowkmrsxonovocohomedobckzzovvozbyqbkwwobmoddoczomspsmkdsyxocdvomyno"
key = CesarFrequencyAttack(text, Counter(text))
print("the key is ", key," and decrypted message is ", Cesar(text, key))
