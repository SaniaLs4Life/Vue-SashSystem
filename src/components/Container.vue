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
                                <option value="hcy">Havalı Çelik Yay +9</option>
                                <option value="ay">Anka Yay +9</option>
                                <option value="zy">Zodyak Yay +9</option>
                                <option value="ky">Kyanit Yay +9</option>
                        </select><br>
                        <!-- SASH RATE LIST ENDS-->

                        <input type="text" class="sashInput" v-model="avgDamage" placeholder="Ortalama Zarar"><br />
                        <input type="text" class="sashInput" v-model="skilBec" placeholder="Beceri Hasarı"><br />
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
                    <div id="sashFeatures">
                        <p class="sashError">Henüz Bir Kuşak Yok.</p>
                        <img class="sashFeatures" draggable="false" src="../image/sash.png" width="250" height="400" alt="">  
                    </div>
                    <div class="sashDetail">
                        <img class="sash3" draggable="false" src="../image/sash3.png" width="350" height="400" alt="">  
                        <ul>
                            <li>Saldırı Değeri 140 - 194</li>
                            <li>Saldırı hızı +%8</li>
                            <li>Ortalama Zarar %14</li>
                            <li>Beceri Hasarı %1</li>
                            <li>Birinci Efsun +2</li>
                            <li>İkinci Efsun +2</li>
                            <li>Üçüncü Efsun +3</li>
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
            skilBec: null,
            firstFeat: null,
            secondFeat: null,
            thirdFeat: null
        }
    },
    methods: {
        showSashAndBow() {
            console.log(this.sashRate + ' ' + this.bowList + ' ' + this.avgDamage * 3)
        }
    }
}
</script>
