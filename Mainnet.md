



<div align="center">
  <h1>CREDIT COIN REHBER </h1>
</div>

<div align="center">
  <img src="https://bitcoinvn.com/attachments/8c8e7200-588d-11ea-9d3c-107e95d9307a-png.2668/" alt="CREDIT COIN Background" />
</div>

 * [Topluluk kanalımız](https://t.me/corenodechat)<br>
 * [Topluluk Twitter](https://twitter.com/corenodeHQ)<br>
 * [CreditCoin Website](https://creditcoin.org/)<br>
 * [Discord](https://discord.com/invite/creditcoin)<br>
 * [Twitter](https://twitter.com/Creditcoin)<br>

## Öncelikle Bu Dökümanızı Okumanızı Tavsiye Ediyorum
* https://creditcoin.org/blog/testnet_live/
* Ayrıca era donguleri gunde bir gerçekleşiyor ve yeni 100 validator seçiliyor. yani bir sıra var ve active geçtiğinizde performansınız ölçülüyor
## Sistem Gereksinimleri
| Bileşenler | Minimum Gereksinimler | 
| ------------ | ------------ |
| CPU |	4 |
| RAM	| 8 GB |
| Storage	| 100 GB SSD |


## Update edelim
```bash
sudo apt update; sudo apt upgrade 
```
## Docker kurulumu
```bash
sudo apt-get update && sudo apt install jq git && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin 

```

##  Dosyaları çekiyoruz 
```bash
docker pull gluwa/creditcoin:2.230.1-mainnet 
```

##  Validatorü oluşturuyoruz (adınızı yazınız kısmını değiştiriniz)
```bash
docker run \
 --name creditcoin-validator \
 -p 30333:30333 \
 -v creditcoin/creditcoin-node/data  \
 gluwa/creditcoin:2.230.1-mainnet `# Enter latest mainnet image` \
 --name "CoreNode" `# name the validator` \
 --telemetry-url "wss://telemetry.creditcoin.network/submit/ 0" `# (optional) opt in to telemetry` \
 --public-addr "/dns4/IPKAMU/tcp/30333" `# REPLACE <yourhostname or ip> with the public IP address or host name at which your node can be reached` \
 --chain main `# we want to connect to the mainnet` \
 --bootnodes "/dns4/bootnode.creditcoin.network/tcp/30333/p2p/12D3KooWAEgDL126EUFxFfdQKiUhmx3BJPdszQHu9PsYsLCuavhb" "/dns4/bootnode2.creditcoin.network/tcp/30333/p2p/12D3KooWSQye3uN3bZQRRC4oZbpiAZXkP2o5UZh6S8pqyh24bF3k" "/dns4/bootnode3.creditcoin.network/tcp/30333/p2p/12D3KooWFrsEZ2aSfiigAxs6ir2kU6en4BewotyCXPhrJ7T1AzjN" \
 --validator `# we want to run a validator node` \
 --base-path /creditcoin-node/data `# the base path to store the node's data` \
 --port 30333 # the port to use for node-to-node communication
```


##  Logları kontrol edelim
eşleşme biteseye kadar beklemeniz gerekiyor. devam etmek için. eşleşme hızlı oluyor pek beklemıyorsunuz 
```bash
docker logs -f creditcoin-validator
```

## Wallet oluşturalım (mnemoniclerinizi mutlaka yedekleyiniz)
```bash
docker exec -it creditcoin-validator creditcoin-cli new
```

## Validatore stake yapıyoruz (eşleşmeden sonra) 
```bash
docker exec -it creditcoin-validator creditcoin-cli wizard -a 1000
```
  
- 5000 değiştirebilirsiniz.
- mnemonickleri isteyecektir
- minimum 1000 CTC
#### Çıktı bu şekilde 
```bash
💰 Stash account: cüzdan adresiniz görünecek
🎮 Controller account: cüzdan adresiniz görünecek
🪙 Amount to bond: 50000.000000000000000000 CTC
🎁 Reward destination: Staked
📡 Node URL: ws://localhost:9944
💸 Commission: 0
🔐 Blocked: No
```

## Telemetry den kontrol (görünmesi zaman alıyor) 
 
- https://telemetry.creditcoin.network/


## Validatorunuze stake etmek için

- https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.mainnet.creditcoin.network%2Fws#/staking/actions
  
* Adrese gidiyoruz. adresimizin sağ kısmında validate yazıyor tıklıyoruz validator komisyon oranını giriyoruz defult 1 dir farketmez. onaylıyoruz. yazmıyorsa sağ yukarıdan calidatr tılayıp cüzdanı ekleriz.
* aynı yerde daha sonra hemen yanında 3 nokta var burdan extra stake işlemi yapabilirsiniz more bond yazıyor.
![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/c9458a40-1611-4098-a999-764d4128e558)

* sol en ustteki menude account yazıyor. buraya gelıp isterseniz cüzdanın yanında 3 noktaya tıklayıp set on identy kısmında twiter github site linki ad değiştirme işlemlerini yapabilirsiniz
![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/3a531b2a-5471-4a0e-87a9-d4fa3eccc7bc)


## Nominator işlemi ( node kurmayanlar için)

* geldikten sonra https://staking.creditcoin.org/#/overview   adresine giriyoruz. sol taraftan testnette ise mainnete almamız lazım.
![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/b9a93a95-0103-4329-b716-bd4b6ad71841)
![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/cc18b0fb-1223-4a44-96e1-3e8e5a1e41ec)
* sağ üstten cüzdanı bağlıyoruz. seçin sona tekrar tıklayıp seçin
* validator tıklıyoruz soldan. arama yerine molla yazıyoruz çıkmassa altındaki active validator tıklayın gelir sonra validator gorunucek ve favoriye almak için kalp tıklayınız( core node da arayın olabilir)
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/51e7398e-368d-469e-9f56-f417afaf1e6e)
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/3b6c5453-ac90-499c-8ce6-92f83dcd5ba2)
* tekrar sol menuden owerview diyelim ve gelen sayfada start tıklayalım
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/29e7824b-abb4-46b3-bdad-0b362f7ae796)
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/e345076a-1be8-4616-88ef-60af0d6cdf42)
* çıkan ekrandakine tıklayın
* sağdan start nominating diyelim
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/67cc7303-568a-42cc-bf78-c35fd7c2aa12)
* böyle bir ekran gelecek continue diyelim
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/b6546408-d86c-4d27-a075-13e78bcc8edc)
* sağdan from favorite diyelim. ve select diyerek mollaya tik atalım. (core node da olabilir daha once eklediyseniz birden fazla seçebilirsiniz)
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/bf781350-6610-4c28-9362-c80edfeb41a7)
* continue deyip devam edıyoruz ve bizi stake miktarı yapacağımız ekrana getiriyor.
* ![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/47783786-0bbf-4db8-8d5a-0f8728948103)
* miktarı girin ve devam edin. şuan faucet nominator hesabına gelmedi devamını resimli anlatamıyorum pek bişide kalmadı zaten :D


* 2gün aktive girebildim. çalıştığını onaylamıs olduk bir sorunumuz yok telemetrydede gorunuyorum.hayırlı olsun
![image](https://github.com/molla202/CreditCoin-CTC/assets/91562185/3428f178-ec61-4a49-a242-7180359dc80c)


