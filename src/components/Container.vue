<template>
    <main class="container">
        <section class="sash">
            <div class="box">
                <div class="title">Kuşak Ayarları</div>
                <div class="features">
                    <form @submit.prevent="showSashAndBow()">
                        <!-- SASH RATE LIST STARTS-->
                        <select v-model="sashRate" class="sashInput">
                            <option disabled selected value="selectSash">Kuşak Emiş Oranı Seçiniz</option>
                            <option value="11">Emiş Oranı : 11%</option>
                            <option value="12">Emiş Oranı : 12%</option>
                            <option value="13">Emiş Oranı : 13%</option>
                            <option value="14">Emiş Oranı : 14%</option>
                            <option value="15">Emiş Oranı : 15%</option>
                            <option value="16">Emiş Oranı : 16%</option>
                            <option value="17">Emiş Oranı : 17%</option>
                            <option value="18">Emiş Oranı : 18%</option>
                            <option value="19">Emiş Oranı : 19%</option>
                            <option value="20">Emiş Oranı : 20%</option>
                            <option value="21">Emiş Oranı : 21%</option>
                            <option value="22">Emiş Oranı : 22%</option>
                            <option value="23">Emiş Oranı : 23%</option>
                            <option value="24">Emiş Oranı : 24%</option>
                            <option value="25">Emiş Oranı : 25%</option>
                        </select>
                        <!-- SASH RATE LIST ENDS-->

                        <!-- BOW LIST STARTS-->
                        <select v-model="bowList" class="sashInput">
                                <option disabled selected value="yay">Yay Seçiniz</option>
                                <option value="gby">Geyik Boynuzu Yay +9</option>
                                <option value="fe">Fırtına Elçisi (Genç Kahramanlar Yayı)</option>
                                <option value="hcy">Havalı Çelik Yay +9</option>
                                <option value="ay">Anka Yay +9</option>
                                <option value="zy">Zodyak Yay +9</option>
                                <option value="ky">Kyanit Yay +9</option>
                        </select><br>
                        <!-- SASH RATE LIST ENDS-->

                        <input type="text" :class="{ 'sashInputError' : error }" class="sashInput" v-if="feats" v-model="avgDamage" placeholder="Ort. Zarar veya Bec. Hasarı"><br />
                        <input type="text" class="sashInput" v-model="firstFeat" placeholder="1. Efsun Oranı"><br />
                        <input type="text" class="sashInput" v-model="secondFeat" placeholder="2. Efsun Oranı"><br />
                        <input type="text" class="sashInput" v-model="thirdFeat" placeholder="3. Efsun Oranı"><br />


                        <input type="submit" class="sashButton" value="Hesapla" >
                    </form>
                </div>                
            </div>
            <div class="box">
                <div class="title">Kuşak Sonucu</div>
                <div class="features">
                    <div id="sashFeatures" v-if="noSash">
                        <p class="sashError">Henüz Bir Kuşak Yok.</p>
                        <img class="sashFeatures" draggable="false" src="../image/sash.png" width="320" height="400" alt="">  
                    </div>
                    <div class="sashDetail" v-if="sashFeat">
                        <img class="sash3" draggable="false" src="../image/sash3.png" width="320" height="400" alt="">  
                        <ul>
                            <li>Saldırı Değeri {{ newAttackValue }} - {{ newAttackValue2 }}</li>
                            <li>Saldırı hızı +%{{ attackSpeed }} </li>       
                            <li v-if="kyanitFeat">Yarı İnsanlara Karşı Güçlü +{{ newKyanitHalfHuman }}</li>
                            <li v-if="kyanitFeat">Canavarlara Karşı Güçlü +{{ newKyanitMonster }}</li>
                            <li v-if="feats">Ort. Zarar veya Bec. Hasarı %{{ newAvgDamage }}</li>
                            <li v-if="plusFeat">Kritik Vuruş Şansı +%{{ newCriticChange }}</li>
                            <li v-if="plusFeat">Saldırı Değeri +%{{ newAttackValuePlus }}</li>
                            <li>1. Efsun Oranı +{{ newFirstFeat }}</li>
                            <li>2. Efsun Oranı +{{ newSecondFeat }}</li>
                            <li>3. Efsun Oranı +{{ newThirdFeat }}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>

<script>
export default {
    name: 'Container',
    data() {
        return {
            sashRate: null,
            bowList: null,
            avgDamage: null,
            firstFeat: null,
            secondFeat: null,
            thirdFeat: null,
            sashFeat: false,
            noSash: true,
            isAvailable: false,
            feats: true,
            plusFeat: false,
            error: false,

            //NEW VALUES
            newAttackValue: null,
            newAttackValue2: null,
            newAttackSpeed: null,
            newCriticChange: null,
            newAttackValuePlus: null,
            newAvgDamage: null,
            newFirstFeat: null,
            newSecondFeat: null,
            newThirdFeat: null,

            newKyanitHalfHuman: null,
            newKyanitMonster: null,
            kyanitFeat: false,

            //BOW LIST
            geyikBoynuz: {
                attack1:164,
                attack2:257,
                attackSpeed:15
            },
            firtinaYay: {
                attack1:120,
                attack2:186,
                attackSpeed:26,
                criticChance: 6,
                attackValuePlus: 35
            },
            havaliCelik: {
                attack1:280,
                attack2:380,
                attackSpeed:26
            },
            ankaYay: {
                attack1:487,
                attack2:686,
                attackSpeed:15
            },
            zodyakYay: {
                attack1:487,
                attack2:686,
                attackSpeed:27
            },
            kyanitYay: {
                attack1:528,
                attack2:734,
                attackSpeed:25,
                halfHuman: 20,
                monster: 5
            },
            


        }
    },
    methods: {
        showSashAndBow() {
            if(this.sashRate && this.bowList) {
                if(this.bowList === 'gby' || this.bowList == 'fe' || this.bowList == 'hcy' || this.bowList == 'zy') {
                    this.sashFeat = true
                    this.noSash = false
                    this.error = false
                    this.sashCalculator()
                }else {
                    this.sashFeat = true
                    this.noSash = false
                    this.sashCalculator()
                }
            }else {
                this.error = true
                this.noSash = true
                this.sashFeat = false
            }
            
            
        },
        sashCalculator() {
            this.newAvgDamage = Math.floor(this.avgDamage * this.sashRate / 100)
            this.newFirstFeat = Math.floor(this.firstFeat * this.sashRate / 100)
            this.newSecondFeat = Math.floor(this.secondFeat * this.sashRate / 100)
            this.newThirdFeat = Math.floor(this.thirdFeat * this.sashRate / 100)
        }
    },
    watch: {
        sashRate() {
            this.newAvgDamage = Math.floor(this.avgDamage * this.sashRate / 100)
            if(this.bowList === 'gby') {
                this.newAttackValue = Math.floor(this.geyikBoynuz.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.geyikBoynuz.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.geyikBoynuz.attackSpeed * this.sashRate / 100)
            }
            if(this.bowList === 'fe') {
                this.newAttackValue = Math.floor(this.firtinaYay.attack1 * this.sashRate / 100) - 14
                this.newAttackValue2 = Math.floor(this.firtinaYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.firtinaYay.attackSpeed * this.sashRate / 100)
                this.newCriticChange = Math.floor(this.firtinaYay.criticChance * this.sashRate / 100)
                this.newAttackValuePlus = Math.floor(this.firtinaYay.attackValuePlus * this.sashRate / 100) - 2
            }
            if(this.bowList === 'hcy') {
                this.newAttackValue = Math.floor(this.havaliCelik.attack1 * this.sashRate / 100) 
                this.newAttackValue2 = Math.floor(this.havaliCelik.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.havaliCelik.attackSpeed * this.sashRate / 100)
            }
            if(this.bowList === 'ay') {
                this.newAttackValue = Math.floor(this.ankaYay.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.ankaYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.ankaYay.attackSpeed * this.sashRate / 100)
            }
            if(this.bowList === 'zy') {
                this.newAttackValue = Math.floor(this.zodyakYay.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.zodyakYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.zodyakYay.attackSpeed * this.sashRate / 100)
            }
            if(this.bowList === 'ky') {
                this.newAttackValue = Math.floor(this.kyanitYay.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.kyanitYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.kyanitYay.attackSpeed * this.sashRate / 100)
                this.newKyanitHalfHuman = Math.floor(this.kyanitYay.halfHuman * this.sashRate / 100)
                this.newKyanitMonster = Math.floor(this.kyanitYay.monster * this.sashRate / 100)
                this.newFirstFeat = Math.floor(this.firstFeat * this.sashRate / 100)
                this.newSecondFeat = Math.floor(this.secondFeat * this.sashRate / 100)
                this.newThirdFeat = Math.floor(this.thirdFeat * this.sashRate / 100)
            }



            
        
            
        },
        bowList() {
            if(this.bowList === 'gby') {
                this.newAttackValue = Math.floor(this.geyikBoynuz.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.geyikBoynuz.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.geyikBoynuz.attackSpeed * this.sashRate / 100)
                
                
                this.isAvailable = false                
                this.kyanitFeat = false
                this.feats = true
                this.plusFeat = false
                

            }
            if(this.bowList === 'fe') {
                this.newAttackValue = Math.floor(this.firtinaYay.attack1 * this.sashRate / 100) - 14
                this.newAttackValue2 = Math.floor(this.firtinaYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.firtinaYay.attackSpeed * this.sashRate / 100)
                this.newCriticChange = Math.floor(this.firtinaYay.criticChance * this.sashRate / 100)
                this.newAttackValuePlus = Math.floor(this.firtinaYay.attackValuePlus * this.sashRate / 100) - 2

                this.isAvailable = false                
                this.kyanitFeat = false
                this.feats = true
                this.plusFeat = true
            }
            if(this.bowList === 'hcy') {
                this.newAttackValue = Math.floor(this.havaliCelik.attack1 * this.sashRate / 100) 
                this.newAttackValue2 = Math.floor(this.havaliCelik.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.havaliCelik.attackSpeed * this.sashRate / 100)

                this.isAvailable = false                
                this.kyanitFeat = false
                this.feats = true
                this.plusFeat = false
            }
            if(this.bowList === 'ay') {
                this.newAttackValue = Math.floor(this.ankaYay.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.ankaYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.ankaYay.attackSpeed * this.sashRate / 100)

                this.isAvailable = true
                this.kyanitFeat = true
                this.feats = false
                this.plusFeat = false
            }
            if(this.bowList === 'zy') {
                this.newAttackValue = Math.floor(this.zodyakYay.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.zodyakYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.zodyakYay.attackSpeed * this.sashRate / 100)

                this.isAvailable = false                
                this.kyanitFeat = false
                this.feats = true
                this.plusFeat = false
            }
            if(this.bowList === 'ky') {
                this.newAttackValue = Math.floor(this.kyanitYay.attack1 * this.sashRate / 100)
                this.newAttackValue2 = Math.floor(this.kyanitYay.attack2 * this.sashRate / 100)
                this.attackSpeed = Math.floor(this.kyanitYay.attackSpeed * this.sashRate / 100)
                this.newKyanitHalfHuman = Math.floor(this.kyanitYay.halfHuman * this.sashRate / 100)
                this.newKyanitMonster = Math.floor(this.kyanitYay.monster * this.sashRate / 100)
                this.newFirstFeat = Math.floor(this.firstFeat * this.sashRate / 100)
                this.newSecondFeat = Math.floor(this.secondFeat * this.sashRate / 100)
                this.newThirdFeat = Math.floor(this.thirdFeat * this.sashRate / 100)

                this.isAvailable = true
                this.kyanitFeat = true
                this.feats = false
                this.plusFeat = false
            }
        }
    }
}
</script>
