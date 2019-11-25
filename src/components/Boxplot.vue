<template>
  <div class="hello">
    <div id="boxplot"/>
  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  name: "Boxplot",
  props: {
    chartData: {
      type: Object
    }
  },
  mounted() {
    this.grabData();
  },
  data() {
    const width = 800;
    const height = 350;
    const margin = { top: 80, right: 25, bottom: 70, left: 60 };
    const tableData = [
      { stain: "CCR2", value: -0.3608166663757804, slide_id: 110035 },
      { stain: "CCR2", value: -0.32319089036172005, slide_id: 110036 },
      { stain: "CCR2", value: -0.283456665258146, slide_id: 110037 },
      { stain: "CCR2", value: -0.43892340987928435, slide_id: 110038 },
      { stain: "CCR2", value: -0.33736017025494025, slide_id: 110039 },
      { stain: "CCR2", value: -0.3240756859617838, slide_id: 110040 },
      { stain: "CCR2", value: -0.3490068414160637, slide_id: 110041 },
      { stain: "CCR2", value: 0.10692644875297995, slide_id: 110042 },
      { stain: "CCR2", value: -0.38579802299885824, slide_id: 110043 },
      { stain: "CCR2", value: -0.41217246205607905, slide_id: 110044 },
      { stain: "CCR2", value: -0.31890496557559544, slide_id: 110045 },
      { stain: "CCR2", value: -0.41028364308005627, slide_id: 110046 },
      { stain: "CCR2", value: 0.039700808586430755, slide_id: 110047 },
      { stain: "CCR2", value: -0.06470507222109706, slide_id: 110048 },
      { stain: "CCR2", value: -0.37597114420666033, slide_id: 110049 },
      { stain: "CCR2", value: -0.43608076869610074, slide_id: 110050 },
      { stain: "CCR2", value: -0.44152132036457803, slide_id: 110051 },
      { stain: "CCR2", value: -0.42930361090837804, slide_id: 110052 },
      { stain: "CCR2", value: -0.42127769904680645, slide_id: 110053 },
      { stain: "CCR2", value: -0.19284355557785376, slide_id: 110054 },
      { stain: "CD137", value: -0.4357670113911136, slide_id: 110055 },
      { stain: "CD137", value: -0.4408938057546038, slide_id: 110056 },
      { stain: "CD137", value: -0.405671410696745, slide_id: 110057 },
      { stain: "CD137", value: -0.43720401984795476, slide_id: 110058 },
      { stain: "CD137", value: -0.4355034552549244, slide_id: 110059 },
      { stain: "CD137", value: -0.29128177244452574, slide_id: 110060 },
      { stain: "CD137", value: -0.42481060630096185, slide_id: 110061 },
      { stain: "CD137", value: -0.3694951934317253, slide_id: 110062 },
      { stain: "CD137", value: -0.3833758166043573, slide_id: 110063 },
      { stain: "CD137", value: -0.4348822157910498, slide_id: 110064 },
      { stain: "CD137", value: -0.35463564746753334, slide_id: 110065 },
      { stain: "CD137", value: -0.4189809955743004, slide_id: 110066 },
      { stain: "CD137", value: -0.3932466214192535, slide_id: 110067 },
      { stain: "CD137", value: -0.4008771990765412, slide_id: 110068 },
      { stain: "CD137", value: -0.42098904232621825, slide_id: 110069 },
      { stain: "CD137", value: -0.3910754208687423, slide_id: 110070 },
      { stain: "CD137", value: -0.4415526960950768, slide_id: 110071 },
      { stain: "CD137", value: -0.42863217027570544, slide_id: 110072 },
      { stain: "CD137", value: -0.43525244941093455, slide_id: 110073 },
      { stain: "CD137", value: -0.35702647813153554, slide_id: 110074 },
      { stain: "CD163+CD68", value: -0.20649199834479526, slide_id: 110075 },
      { stain: "CD163+CD68", value: -0.32940328500046584, slide_id: 110076 },
      { stain: "CD163+CD68", value: 0.0419222103057399, slide_id: 110077 },
      { stain: "CD163+CD68", value: -0.09790687023483846, slide_id: 110078 },
      { stain: "CD163+CD68", value: -0.23565887741640176, slide_id: 110079 },
      { stain: "CD163+CD68", value: 0.4163539029313185, slide_id: 110080 },
      { stain: "CD163+CD68", value: -0.03402588293945239, slide_id: 110081 },
      { stain: "CD163+CD68", value: 1.5426798763742302, slide_id: 110082 },
      { stain: "CD163+CD68", value: 0.10114703919511649, slide_id: 110083 },
      { stain: "CD163+CD68", value: 0.0025268430915518845, slide_id: 110084 },
      { stain: "CD163+CD68", value: 0.3118978209549927, slide_id: 110085 },
      { stain: "CD163+CD68", value: -0.13190561180324725, slide_id: 110086 },
      { stain: "CD163+CD68", value: 0.09093737649083423, slide_id: 110087 },
      { stain: "CD163+CD68", value: 0.09455813579038605, slide_id: 110088 },
      { stain: "CD163+CD68", value: 0.17690060291121673, slide_id: 110089 },
      { stain: "CD163+CD68", value: 0.4106874460032503, slide_id: 110090 },
      { stain: "CD163+CD68", value: -0.3950538634959795, slide_id: 110091 },
      { stain: "CD163+CD68", value: -0.132620978458618, slide_id: 110092 },
      { stain: "CD163+CD68", value: -0.16588552793335684, slide_id: 110093 },
      { stain: "CD163+CD68", value: 0.2819088977443199, slide_id: 110094 },
      { stain: "CD28", value: -0.2951723630263665, slide_id: 110095 },
      { stain: "CD28", value: -0.43402879592148463, slide_id: 110096 },
      { stain: "CD28", value: 0.8623661871166681, slide_id: 110097 },
      { stain: "CD28", value: -0.33971962518844373, slide_id: 110098 },
      { stain: "CD28", value: 0.582620173990115, slide_id: 110099 },
      { stain: "CD28", value: -0.17972222508329067, slide_id: 110100 },
      { stain: "CD28", value: -0.3875927147833848, slide_id: 110101 },
      { stain: "CD28", value: 0.13964506051704112, slide_id: 110102 },
      { stain: "CD28", value: -0.04821398827097183, slide_id: 110103 },
      { stain: "CD28", value: 0.1702363977532894, slide_id: 110104 },
      { stain: "CD28", value: -0.08376896607211698, slide_id: 110105 },
      { stain: "CD28", value: -0.3718232726347301, slide_id: 110106 },
      { stain: "CD28", value: -0.11492506645734209, slide_id: 110107 },
      { stain: "CD28", value: -0.2236858986580917, slide_id: 110108 },
      { stain: "CD28", value: 0.31339130572673163, slide_id: 110109 },
      { stain: "CD28", value: -0.004909205036643787, slide_id: 110110 },
      { stain: "CD28", value: -0.30425877457879474, slide_id: 110111 },
      { stain: "CD28", value: -0.1482272668086794, slide_id: 110112 },
      { stain: "CD28", value: -0.19008249129396673, slide_id: 110113 },
      { stain: "CD28", value: 0.1735622251861533, slide_id: 110114 },
      { stain: "CD3", value: -0.34765140985851917, slide_id: 110115 },
      { stain: "CD3", value: -0.3969175818876033, slide_id: 110116 },
      { stain: "CD3", value: -0.30622917045411413, slide_id: 110117 },
      { stain: "CD3", value: -0.43742992510754547, slide_id: 110118 },
      { stain: "CD3", value: -0.04705308624251939, slide_id: 110119 },
      { stain: "CD3", value: 0.1908690781292451, slide_id: 110120 },
      { stain: "CD3", value: -0.0992497515001835, slide_id: 110121 },
      { stain: "CD3", value: 0.058752152145251174, slide_id: 110122 },
      { stain: "CD3", value: -0.2829609287162662, slide_id: 110123 },
      { stain: "CD3", value: -0.2863306821718284, slide_id: 110124 },
      { stain: "CD3", value: -0.13526281496660988, slide_id: 110125 },
      { stain: "CD3", value: -0.4361560704492976, slide_id: 110126 },
      { stain: "CD3", value: 0.25419785256785377, slide_id: 110127 },
      { stain: "CD3", value: -0.2975757439825682, slide_id: 110128 },
      { stain: "CD3", value: -0.34404947599726654, slide_id: 110129 },
      { stain: "CD3", value: -0.24394207026806286, slide_id: 110130 },
      { stain: "CD3", value: -0.4414522937574809, slide_id: 110131 },
      { stain: "CD3", value: -0.4121473614716801, slide_id: 110132 },
      { stain: "CD3", value: -0.279666477013901, slide_id: 110133 },
      { stain: "CD3", value: -0.13869531988316944, slide_id: 110134 },
      { stain: "CD33", value: 0.3023156728606848, slide_id: 110135 },
      { stain: "CD33", value: -0.2797229533287987, slide_id: 110136 },
      { stain: "CD33", value: 0.15366373690386748, slide_id: 110137 },
      { stain: "CD33", value: -0.15854360699665726, slide_id: 110138 },
      { stain: "CD33", value: 0.13188897993775855, slide_id: 110139 },
      { stain: "CD33", value: 0.6939349906534602, slide_id: 110140 },
      { stain: "CD33", value: 0.7474619868842699, slide_id: 110141 },
      { stain: "CD33", value: 8.719457793166864, slide_id: 110142 },
      { stain: "CD33", value: 1.0932539127106204, slide_id: 110143 },
      { stain: "CD33", value: 0.3494482952158562, slide_id: 110144 },
      { stain: "CD33", value: 1.0964103111987913, slide_id: 110145 },
      { stain: "CD33", value: 0.06534733069608137, slide_id: 110146 },
      { stain: "CD33", value: 1.1585781836089475, slide_id: 110147 },
      { stain: "CD33", value: 1.2325809815632194, slide_id: 110148 },
      { stain: "CD33", value: 0.35648900913976816, slide_id: 110149 },
      { stain: "CD33", value: 3.30347959681608, slide_id: 110150 },
      { stain: "CD33", value: -0.3817819294950226, slide_id: 110151 },
      { stain: "CD33", value: 2.546025536554375, slide_id: 110152 },
      { stain: "CD33", value: 0.4936950786106538, slide_id: 110153 },
      { stain: "CD33", value: 0.016470217725181348, slide_id: 110154 },
      { stain: "CD38", value: -0.3780795932961741, slide_id: 110155 },
      { stain: "CD38", value: -0.34390514763697244, slide_id: 110156 },
      { stain: "CD38", value: -0.4039331952271161, slide_id: 110157 },
      { stain: "CD38", value: -0.44169702445537085, slide_id: 110158 },
      { stain: "CD38", value: -0.32935935897776764, slide_id: 110159 },
      { stain: "CD38", value: -0.19770679380515474, slide_id: 110160 },
      { stain: "CD38", value: -0.19223486640617862, slide_id: 110161 },
      { stain: "CD38", value: 0.016758874445769564, slide_id: 110162 },
      { stain: "CD38", value: -0.21097872780611168, slide_id: 110163 },
      { stain: "CD38", value: -0.3798680099346009, slide_id: 110164 },
      { stain: "CD38", value: -0.4333510801427124, slide_id: 110165 },
      { stain: "CD38", value: -0.41876136546080944, slide_id: 110166 },
      { stain: "CD38", value: -0.176145391806437, slide_id: 110167 },
      { stain: "CD38", value: 0.06411112691443194, slide_id: 110168 },
      { stain: "CD38", value: -0.42881414951259805, slide_id: 110169 },
      { stain: "CD38", value: -0.4271826115266648, slide_id: 110170 },
      { stain: "CD38", value: -0.43970152799565254, slide_id: 110171 },
      { stain: "CD38", value: -0.4322717550135566, slide_id: 110172 },
      { stain: "CD38", value: -0.3555894696746943, slide_id: 110173 },
      { stain: "CD38", value: -0.24573676205258943, slide_id: 110174 },
      { stain: "CD39", value: 2.2638008407184227, slide_id: 110175 },
      { stain: "CD39", value: -0.07129397562582741, slide_id: 110176 },
      { stain: "CD39", value: 1.0050441839865298, slide_id: 110177 },
      { stain: "CD39", value: -0.04874110054335026, slide_id: 110178 },
      { stain: "CD39", value: -0.2656854515036731, slide_id: 110179 },
      { stain: "CD39", value: 2.3730762348993513, slide_id: 110180 },
      { stain: "CD39", value: 3.1015767710568416, slide_id: 110181 },
      { stain: "CD39", value: 6.802651665539298, slide_id: 110182 },
      { stain: "CD39", value: 1.1175136275322277, slide_id: 110183 },
      { stain: "CD39", value: 0.30480690586228293, slide_id: 110184 },
      { stain: "CD39", value: 0.44806849131942084, slide_id: 110185 },
      { stain: "CD39", value: -0.21840850078820764, slide_id: 110186 },
      { stain: "CD39", value: 0.17613503508704798, slide_id: 110187 },
      { stain: "CD39", value: 1.4779517443553791, slide_id: 110188 },
      { stain: "CD39", value: 3.0050587488966913, slide_id: 110189 },
      { stain: "CD39", value: 0.3736013325537678, slide_id: 110190 },
      { stain: "CD39", value: -0.29350944930993456, slide_id: 110191 },
      { stain: "CD39", value: 1.1478602340705861, slide_id: 110192 },
      { stain: "CD39", value: 1.551954542309651, slide_id: 110193 },
      { stain: "CD39", value: 1.6604831941047102, slide_id: 110194 },
      { stain: "CD45", value: -0.326981078605965, slide_id: 110195 },
      { stain: "CD45", value: -0.38185723124821946, slide_id: 110196 },
      { stain: "CD45", value: -0.3383579184847994, slide_id: 110197 },
      { stain: "CD45", value: -0.39260028137097985, slide_id: 110198 },
      { stain: "CD45", value: 0.4186882572804229, slide_id: 110199 },
      { stain: "CD45", value: -0.16355117358425234, slide_id: 110200 },
      { stain: "CD45", value: -0.1304184021776081, slide_id: 110201 },
      { stain: "CD45", value: -0.12010206198963025, slide_id: 110202 },
      { stain: "CD45", value: 0.005425960589633281, slide_id: 110203 },
      { stain: "CD45", value: -0.35643661439815966, slide_id: 110204 },
      { stain: "CD45", value: 0.07277082853207754, slide_id: 110205 },
      { stain: "CD45", value: -0.39665402575141406, slide_id: 110206 },
      { stain: "CD45", value: 0.23327024032521007, slide_id: 110207 },
      { stain: "CD45", value: 0.15498779273091332, slide_id: 110208 },
      { stain: "CD45", value: -0.3113873405481031, slide_id: 110209 },
      { stain: "CD45", value: -0.2325150292204304, slide_id: 110210 },
      { stain: "CD45", value: -0.4087587825778187, slide_id: 110211 },
      { stain: "CD45", value: -0.39996102774597875, slide_id: 110212 },
      { stain: "CD45", value: -0.19379110263891497, slide_id: 110213 },
      { stain: "CD45", value: -0.1395299143144353, slide_id: 110214 },
      { stain: "CD8", value: -0.38660124169962534, slide_id: 110215 },
      { stain: "CD8", value: -0.32548131868812635, slide_id: 110216 },
      { stain: "CD8", value: -0.18306060280835404, slide_id: 110217 },
      { stain: "CD8", value: -0.42747754339335275, slide_id: 110218 },
      { stain: "CD8", value: 0.1385845608261846, slide_id: 110219 },
      { stain: "CD8", value: -0.06516315788637829, slide_id: 110220 },
      { stain: "CD8", value: -0.163657851067948, slide_id: 110221 },
      { stain: "CD8", value: -0.14741777296181252, slide_id: 110222 },
      { stain: "CD8", value: -0.18950517785279034, slide_id: 110223 },
      { stain: "CD8", value: -0.2500791631536117, slide_id: 110224 },
      { stain: "CD8", value: -0.15526798073259132, slide_id: 110225 },
      { stain: "CD8", value: -0.41265564830575924, slide_id: 110226 },
      { stain: "CD8", value: 0.07999352169288199, slide_id: 110227 },
      { stain: "CD8", value: -0.1670527051079091, slide_id: 110228 },
      { stain: "CD8", value: -0.314907697510059, slide_id: 110229 },
      { stain: "CD8", value: -0.2925054259339757, slide_id: 110230 },
      { stain: "CD8", value: -0.43559758244642044, slide_id: 110231 },
      { stain: "CD8", value: -0.40593496683293423, slide_id: 110232 },
      { stain: "CD8", value: -0.2547666972901199, slide_id: 110233 },
      { stain: "CD8", value: -0.0992309260618843, slide_id: 110234 },
      { stain: "FOXP3", value: -0.4301570307779431, slide_id: 110235 },
      { stain: "FOXP3", value: -0.4393626701062664, slide_id: 110236 },
      { stain: "FOXP3", value: -0.4173933836110654, slide_id: 110237 },
      { stain: "FOXP3", value: -0.4420296071986573, slide_id: 110238 },
      { stain: "FOXP3", value: -0.4085642530487267, slide_id: 110239 },
      { stain: "FOXP3", value: -0.3381696641018071, slide_id: 110240 },
      { stain: "FOXP3", value: -0.422143669208571, slide_id: 110241 },
      { stain: "FOXP3", value: -0.3633078993773785, slide_id: 110242 },
      { stain: "FOXP3", value: -0.3909561930928472, slide_id: 110243 },
      { stain: "FOXP3", value: -0.43196427285466915, slide_id: 110244 },
      { stain: "FOXP3", value: -0.38344484321145456, slide_id: 110245 },
      { stain: "FOXP3", value: -0.43439275439526975, slide_id: 110246 },
      { stain: "FOXP3", value: -0.3421543818751441, slide_id: 110247 },
      { stain: "FOXP3", value: -0.37937227339272117, slide_id: 110248 },
      { stain: "FOXP3", value: -0.42509926302155004, slide_id: 110249 },
      { stain: "FOXP3", value: -0.42225662183836643, slide_id: 110250 },
      { stain: "FOXP3", value: -0.4427198732696291, slide_id: 110251 },
      { stain: "FOXP3", value: -0.435145771927239, slide_id: 110252 },
      { stain: "FOXP3", value: -0.4307657199496182, slide_id: 110253 },
      { stain: "FOXP3", value: -0.3904353559665685, slide_id: 110254 },
      { stain: "Granzyme B", value: -0.42632919165709976, slide_id: 110255 },
      { stain: "Granzyme B", value: -0.43871005491189313, slide_id: 110256 },
      { stain: "Granzyme B", value: -0.4357921119755125, slide_id: 110257 },
      { stain: "Granzyme B", value: -0.4381452917629162, slide_id: 110258 },
      { stain: "Granzyme B", value: -0.43577328653721326, slide_id: 110259 },
      { stain: "Granzyme B", value: -0.43771858182813367, slide_id: 110260 },
      { stain: "Granzyme B", value: -0.44149621978017917, slide_id: 110261 },
      { stain: "Granzyme B", value: -0.43813274147071674, slide_id: 110262 },
      { stain: "Granzyme B", value: -0.4382268686622129, slide_id: 110263 },
      { stain: "Granzyme B", value: -0.4296299185055647, slide_id: 110264 },
      { stain: "Granzyme B", value: -0.437197744701855, slide_id: 110265 },
      { stain: "Granzyme B", value: -0.4267182507152838, slide_id: 110266 },
      { stain: "Granzyme B", value: -0.43673338389047395, slide_id: 110267 },
      { stain: "Granzyme B", value: -0.4331816511980193, slide_id: 110268 },
      { stain: "Granzyme B", value: -0.4219554148255787, slide_id: 110269 },
      { stain: "Granzyme B", value: -0.4420484326369565, slide_id: 110270 },
      { stain: "Granzyme B", value: -0.44285165133772364, slide_id: 110271 },
      { stain: "Granzyme B", value: -0.42203699172487535, slide_id: 110272 },
      { stain: "Granzyme B", value: -0.44071182651771124, slide_id: 110273 },
      { stain: "Granzyme B", value: -0.41269329918235775, slide_id: 110274 },
      { stain: "ICOS", value: -0.43897361104808236, slide_id: 110395 },
      { stain: "ICOS", value: -0.4385531762593996, slide_id: 110396 },
      { stain: "ICOS", value: -0.401347835034022, slide_id: 110397 },
      { stain: "ICOS", value: -0.4135341687597233, slide_id: 110398 },
      { stain: "ICOS", value: -0.4145632927200812, slide_id: 110399 },
      { stain: "ICOS", value: -0.22221123932465203, slide_id: 110400 },
      { stain: "ICOS", value: -0.39951549237289696, slide_id: 110401 },
      { stain: "ICOS", value: -0.3605154593629928, slide_id: 110402 },
      { stain: "ICOS", value: -0.3721495802319167, slide_id: 110403 },
      { stain: "ICOS", value: -0.42087608969642293, slide_id: 110404 },
      { stain: "ICOS", value: -0.25159147336364984, slide_id: 110405 },
      { stain: "ICOS", value: -0.4040524230030113, slide_id: 110406 },
      { stain: "ICOS", value: -0.3505756279409995, slide_id: 110407 },
      { stain: "ICOS", value: -0.37568248748607214, slide_id: 110408 },
      { stain: "ICOS", value: -0.4215412551829957, slide_id: 110409 },
      { stain: "ICOS", value: -0.4309853500631092, slide_id: 110410 },
      { stain: "ICOS", value: -0.44288930221432216, slide_id: 110411 },
      { stain: "ICOS", value: -0.4284376407466135, slide_id: 110412 },
      { stain: "ICOS", value: -0.41021461647295915, slide_id: 110413 },
      { stain: "ICOS", value: -0.24728672313922598, slide_id: 110414 },
      { stain: "LAG3", value: -0.44076202768650913, slide_id: 110415 },
      { stain: "LAG3", value: -0.442086083513555, slide_id: 110416 },
      { stain: "LAG3", value: -0.4195583090154768, slide_id: 110417 },
      { stain: "LAG3", value: -0.44058004844961657, slide_id: 110418 },
      { stain: "LAG3", value: -0.4420484326369565, slide_id: 110419 },
      { stain: "LAG3", value: -0.42432742005128166, slide_id: 110420 },
      { stain: "LAG3", value: -0.4366769075755763, slide_id: 110421 },
      { stain: "LAG3", value: -0.43582348770601126, slide_id: 110422 },
      { stain: "LAG3", value: -0.4291592825480839, slide_id: 110423 },
      { stain: "LAG3", value: -0.38960076153530265, slide_id: 110424 },
      { stain: "LAG3", value: -0.42365597941860916, slide_id: 110425 },
      { stain: "LAG3", value: -0.43931874408356825, slide_id: 110426 },
      { stain: "LAG3", value: -0.4310355512319072, slide_id: 110427 },
      { stain: "LAG3", value: -0.43966387711905414, slide_id: 110428 },
      { stain: "LAG3", value: -0.44116363703689276, slide_id: 110429 },
      { stain: "LAG3", value: -0.44107578499149636, slide_id: 110430 },
      { stain: "LAG3", value: -0.4417221250397699, slide_id: 110431 },
      { stain: "LAG3", value: -0.43907401338567825, slide_id: 110432 },
      { stain: "LAG3", value: -0.4393877706906654, slide_id: 110433 },
      { stain: "LAG3", value: -0.4190939482040958, slide_id: 110434 },
      { stain: "NKG2D", value: -0.4103589448332532, slide_id: 110435 },
      { stain: "NKG2D", value: -0.41188380533549085, slide_id: 110436 },
      { stain: "NKG2D", value: -0.3595867377402308, slide_id: 110437 },
      { stain: "NKG2D", value: -0.42641704370249617, slide_id: 110438 },
      { stain: "NKG2D", value: -0.3268116496612719, slide_id: 110439 },
      { stain: "NKG2D", value: -0.402445985601477, slide_id: 110440 },
      { stain: "NKG2D", value: -0.412906654149749, slide_id: 110441 },
      { stain: "NKG2D", value: -0.250512148234494, slide_id: 110442 },
      { stain: "NKG2D", value: -0.294281292280203, slide_id: 110443 },
      { stain: "NKG2D", value: -0.39802828274725777, slide_id: 110444 },
      { stain: "NKG2D", value: -0.3813489444141403, slide_id: 110445 },
      { stain: "NKG2D", value: -0.42978679715805823, slide_id: 110446 },
      { stain: "NKG2D", value: -0.15787216636398474, slide_id: 110447 },
      { stain: "NKG2D", value: -0.3607162640381846, slide_id: 110448 },
      { stain: "NKG2D", value: -0.35396420683486085, slide_id: 110449 },
      { stain: "NKG2D", value: -0.36926928817213456, slide_id: 110450 },
      { stain: "NKG2D", value: -0.44049219640422016, slide_id: 110451 },
      { stain: "NKG2D", value: -0.4075602296727677, slide_id: 110452 },
      { stain: "NKG2D", value: -0.41153867230000496, slide_id: 110453 },
      { stain: "NKG2D", value: -0.1369633795596403, slide_id: 110454 },
      { stain: "NKp46", value: -0.43773740726643295, slide_id: 110455 },
      { stain: "NKp46", value: -0.4364384520237861, slide_id: 110456 },
      { stain: "NKp46", value: -0.4399462586935426, slide_id: 110457 },
      { stain: "NKp46", value: -0.4418664534000639, slide_id: 110458 },
      { stain: "NKp46", value: -0.43878535666509005, slide_id: 110459 },
      { stain: "NKp46", value: -0.44225551245824807, slide_id: 110460 },
      { stain: "NKp46", value: -0.4426382963703324, slide_id: 110461 },
      { stain: "NKp46", value: -0.4419166545688619, slide_id: 110462 },
      { stain: "NKp46", value: -0.44160917240997444, slide_id: 110463 },
      { stain: "NKp46", value: -0.43016330592404284, slide_id: 110464 },
      { stain: "NKp46", value: -0.4428830270682224, slide_id: 110465 },
      { stain: "NKp46", value: -0.44239356567244237, slide_id: 110466 },
      { stain: "NKp46", value: -0.44157152153337603, slide_id: 110467 },
      { stain: "NKp46", value: -0.4409189063390027, slide_id: 110468 },
      { stain: "NKp46", value: -0.4397266285800515, slide_id: 110469 },
      { stain: "NKp46", value: -0.44194175515326095, slide_id: 110470 },
      { stain: "NKp46", value: -0.44295205367531953, slide_id: 110471 },
      { stain: "NKp46", value: -0.44273242356182857, slide_id: 110472 },
      { stain: "NKp46", value: -0.44190410427666243, slide_id: 110473 },
      { stain: "NKp46", value: -0.43226547986745684, slide_id: 110474 },
      { stain: "PD1", value: -0.43833982129200827, slide_id: 110475 },
      { stain: "PD1", value: -0.4394128712750644, slide_id: 110476 },
      { stain: "PD1", value: -0.4299562261027513, slide_id: 110477 },
      { stain: "PD1", value: -0.44169702445537085, slide_id: 110478 },
      { stain: "PD1", value: -0.3503246220970098, slide_id: 110479 },
      { stain: "PD1", value: -0.37615939858965264, slide_id: 110480 },
      { stain: "PD1", value: -0.42682492819897944, slide_id: 110481 },
      { stain: "PD1", value: -0.4137914497498128, slide_id: 110482 },
      { stain: "PD1", value: -0.3879880489876686, slide_id: 110483 },
      { stain: "PD1", value: -0.4406804507872125, slide_id: 110484 },
      { stain: "PD1", value: -0.35643661439815966, slide_id: 110485 },
      { stain: "PD1", value: -0.43786291018842777, slide_id: 110486 },
      { stain: "PD1", value: -0.3487934864486724, slide_id: 110487 },
      { stain: "PD1", value: -0.42658019750108944, slide_id: 110488 },
      { stain: "PD1", value: -0.44168447416317147, slide_id: 110489 },
      { stain: "PD1", value: -0.43833982129200827, slide_id: 110490 },
      { stain: "PD1", value: -0.44193548000716115, slide_id: 110491 },
      { stain: "PD1", value: -0.4396387765346551, slide_id: 110492 },
      { stain: "PD1", value: -0.4383147207076093, slide_id: 110493 },
      { stain: "PD1", value: -0.3805080748367747, slide_id: 110494 },
      { stain: "PSGL1", value: -0.3604778084863943, slide_id: 110495 },
      { stain: "PSGL1", value: -0.39452675122360104, slide_id: 110496 },
      { stain: "PSGL1", value: -0.3485487557507824, slide_id: 110497 },
      { stain: "PSGL1", value: -0.3941251418732175, slide_id: 110498 },
      { stain: "PSGL1", value: -0.26535914390648646, slide_id: 110499 },
      { stain: "PSGL1", value: -0.3298425452274479, slide_id: 110500 },
      { stain: "PSGL1", value: -0.3135271653681155, slide_id: 110501 },
      { stain: "PSGL1", value: 2.2352614762567904, slide_id: 110502 },
      { stain: "PSGL1", value: -0.30289706787515047, slide_id: 110503 },
      { stain: "PSGL1", value: -0.36206542044962936, slide_id: 110504 },
      { stain: "PSGL1", value: -0.229421382193257, slide_id: 110505 },
      { stain: "PSGL1", value: -0.3570955047386327, slide_id: 110506 },
      { stain: "PSGL1", value: 0.013395396136307138, slide_id: 110507 },
      { stain: "PSGL1", value: -0.23248992863603146, slide_id: 110508 },
      { stain: "PSGL1", value: -0.4021949797574873, slide_id: 110509 },
      { stain: "PSGL1", value: 0.03034456575171365, slide_id: 110510 },
      { stain: "PSGL1", value: 0.037699036980612666, slide_id: 110511 },
      { stain: "PSGL1", value: 0.021728790156766205, slide_id: 110512 },
      { stain: "PSGL1", value: -0.3764292298719416, slide_id: 110513 },
      { stain: "PSGL1", value: 0.13094143287669727, slide_id: 110514 },
      { stain: "TIGIT", value: -0.4361937213258961, slide_id: 110515 },
      { stain: "TIGIT", value: -0.4416279978482737, slide_id: 110516 },
      { stain: "TIGIT", value: -0.40228910694898345, slide_id: 110517 },
      { stain: "TIGIT", value: -0.436902812835167, slide_id: 110518 },
      { stain: "TIGIT", value: -0.42763442204584634, slide_id: 110519 },
      { stain: "TIGIT", value: -0.4065813068812078, slide_id: 110520 },
      { stain: "TIGIT", value: -0.43702831575716194, slide_id: 110521 },
      { stain: "TIGIT", value: -0.41364084624341896, slide_id: 110522 },
      { stain: "TIGIT", value: -0.43930619379136876, slide_id: 110523 },
      { stain: "TIGIT", value: -0.39757647222807624, slide_id: 110524 },
      { stain: "TIGIT", value: -0.4220809177475736, slide_id: 110525 },
      { stain: "TIGIT", value: -0.43500144356694487, slide_id: 110526 },
      { stain: "TIGIT", value: -0.417550262263559, slide_id: 110527 },
      { stain: "TIGIT", value: -0.40801204019194925, slide_id: 110528 },
      { stain: "TIGIT", value: -0.4351394967811393, slide_id: 110529 },
      { stain: "TIGIT", value: -0.43944424700556306, slide_id: 110530 },
      { stain: "TIGIT", value: -0.44273242356182857, slide_id: 110531 },
      { stain: "TIGIT", value: -0.4208384388198244, slide_id: 110532 },
      { stain: "TIGIT", value: -0.40338725751643845, slide_id: 110533 },
      { stain: "TIGIT", value: -0.3635275294908695, slide_id: 110534 },
      { stain: "VISTA", value: -0.4322843053057561, slide_id: 110535 },
      { stain: "VISTA", value: -0.41515943159955676, slide_id: 110536 },
      { stain: "VISTA", value: -0.39452675122360104, slide_id: 110537 },
      { stain: "VISTA", value: -0.4413079653971868, slide_id: 110538 },
      { stain: "VISTA", value: -0.43806371486361956, slide_id: 110539 },
      { stain: "VISTA", value: -0.40776730949405926, slide_id: 110540 },
      { stain: "VISTA", value: -0.4305209892517282, slide_id: 110541 },
      { stain: "VISTA", value: 0.0702168440694821, slide_id: 110542 },
      { stain: "VISTA", value: -0.4268688542216777, slide_id: 110543 },
      { stain: "VISTA", value: -0.4401094124921359, slide_id: 110544 },
      { stain: "VISTA", value: -0.4299876018332501, slide_id: 110545 },
      { stain: "VISTA", value: -0.44134561627378527, slide_id: 110546 },
      { stain: "VISTA", value: -0.433043597983825, slide_id: 110547 },
      { stain: "VISTA", value: -0.4384025727530057, slide_id: 110548 },
      { stain: "VISTA", value: -0.392939139260366, slide_id: 110549 },
      { stain: "VISTA", value: -0.4096122024473838, slide_id: 110550 },
      { stain: "VISTA", value: -0.4388167323955887, slide_id: 110551 },
      { stain: "VISTA", value: -0.3870279516344079, slide_id: 110552 },
      { stain: "VISTA", value: -0.43659533067627965, slide_id: 110553 },
      { stain: "VISTA", value: -0.4335079587952059, slide_id: 110554 },
      { stain: "CCR8", value: -0.15985511253150358, slide_id: 135328 },
      { stain: "CCR8", value: -0.38707815280320584, slide_id: 135329 },
      { stain: "CCR8", value: -0.2514283195650565, slide_id: 135330 },
      { stain: "CCR8", value: -0.44152759551067783, slide_id: 135331 },
      { stain: "CCR8", value: -0.41456956786618093, slide_id: 135332 },
      { stain: "CCR8", value: -0.15581391844326895, slide_id: 135333 },
      { stain: "CCR8", value: -0.36377226018875947, slide_id: 135334 },
      { stain: "CCR8", value: -0.07114337211943361, slide_id: 135335 },
      { stain: "CCR8", value: -0.3518369323070479, slide_id: 135336 },
      { stain: "CCR8", value: 0.027702729243721722, slide_id: 135337 },
      { stain: "CCR8", value: -0.2857470935845522, slide_id: 135338 },
      { stain: "CCR8", value: -0.3882516051238578, slide_id: 135339 },
      { stain: "CCR8", value: -0.25971778756281727, slide_id: 135340 },
      { stain: "CCR8", value: -0.34103113072329005, slide_id: 135341 },
      { stain: "CCR8", value: -0.3916464591638189, slide_id: 135342 },
      { stain: "CCR8", value: -0.35739043660532066, slide_id: 135343 },
      { stain: "CCR8", value: -0.20803568428533212, slide_id: 135344 },
      { stain: "CCR8", value: -0.19451274444038544, slide_id: 135345 },
      { stain: "CCR8", value: -0.40040028797296073, slide_id: 135346 },
      { stain: "CCR8", value: -0.19466334794677928, slide_id: 135347 },
      { stain: "CD32B", value: -0.41815267628913433, slide_id: 135348 },
      { stain: "CD32B", value: -0.42554479839463183, slide_id: 135349 },
      { stain: "CD32B", value: -0.4057404373038422, slide_id: 135350 },
      { stain: "CD32B", value: -0.42695043112097436, slide_id: 135351 },
      { stain: "CD32B", value: -0.36180186431344014, slide_id: 135352 },
      { stain: "CD32B", value: -0.3619148169432355, slide_id: 135353 },
      { stain: "CD32B", value: -0.3314552577750819, slide_id: 135354 },
      { stain: "CD32B", value: 3.388263095769711, slide_id: 135355 },
      { stain: "CD32B", value: 0.20727858518007367, slide_id: 135356 },
      { stain: "CD32B", value: -0.37937227339272117, slide_id: 135357 },
      { stain: "CD32B", value: -0.20107654726071683, slide_id: 135358 },
      { stain: "CD32B", value: -0.4151280558690581, slide_id: 135359 },
      { stain: "CD32B", value: 0.3427715397657293, slide_id: 135360 },
      { stain: "CD32B", value: -0.09839633163061844, slide_id: 135361 },
      { stain: "CD32B", value: -0.29962771675718425, slide_id: 135362 },
      { stain: "CD32B", value: -0.40228910694898345, slide_id: 135363 },
      { stain: "CD32B", value: -0.44230571362704596, slide_id: 135364 },
      { stain: "CD32B", value: -0.361463006424054, slide_id: 135365 },
      { stain: "CD32B", value: -0.3012906304736162, slide_id: 135366 },
      { stain: "CD32B", value: 0.6851811618443183, slide_id: 135367 },
      { stain: "CD4", value: -0.19143792285151126, slide_id: 135368 },
      { stain: "CD4", value: -0.2971302086094864, slide_id: 135369 },
      { stain: "CD4", value: -0.3309218703566037, slide_id: 135370 },
      { stain: "CD4", value: -0.3775524810237956, slide_id: 135371 },
      { stain: "CD4", value: -0.24505277112771737, slide_id: 135372 },
      { stain: "CD4", value: 0.15951844821492794, slide_id: 135373 },
      { stain: "CD4", value: -0.11454855769135751, slide_id: 135374 },
      { stain: "CD4", value: 0.8067370169424444, slide_id: 135375 },
      { stain: "CD4", value: 0.28573673686516327, slide_id: 135376 },
      { stain: "CD4", value: -0.3515733761708587, slide_id: 135377 },
      { stain: "CD4", value: 0.047488264896212135, slide_id: 135378 },
      { stain: "CD4", value: -0.3942694702335116, slide_id: 135379 },
      { stain: "CD4", value: 0.03890386503176335, slide_id: 135380 },
      { stain: "CD4", value: -0.1607712838620661, slide_id: 135381 },
      { stain: "CD4", value: -0.2446888126539323, slide_id: 135382 },
      { stain: "CD4", value: -0.21713464612995978, slide_id: 135383 },
      { stain: "CD4", value: -0.4351332216350395, slide_id: 135384 },
      { stain: "CD4", value: -0.2741882744688252, slide_id: 135385 },
      { stain: "CD4", value: -0.19297533364594832, slide_id: 135386 },
      { stain: "CD4", value: 0.21063578834343627, slide_id: 135387 }
    ];
    return {
      width,
      height,
      tableData,
      margin
    };
  },
  computed: {},
  methods: {
    async grabData() {
      // append the svg object to the body of the page
      const svg = d3
        .select("#boxplot")
        .append("svg")
        .attr("width", this.width + this.margin.left + this.margin.right)
        .attr("height", this.height + this.margin.top + this.margin.bottom)
        .append("g")
        .attr(
          "transform",
          "translate(" + this.margin.left + "," + this.margin.top + ")"
        );

      // Compute quartiles, median, interquantile range, min, and max --> these info are then used to draw the box.
      const sumstat = d3
        .nest() // nest function allows to group the calculation per level of a factor
        .key(function(d) {
          return d.stain;
        })
        .rollup(function(d) {
          const q1 = d3.quantile(
            d
              .map(function(g) {
                return g.value;
              })
              .sort(d3.ascending),
            0.25
          );
          const median = d3.quantile(
            d
              .map(function(g) {
                return g.value;
              })
              .sort(d3.ascending),
            0.5
          );
          const q3 = d3.quantile(
            d
              .map(function(g) {
                return g.value;
              })
              .sort(d3.ascending),
            0.75
          );
          const interQuantileRange = q3 - q1;
          const min = q1 - 1.5 * interQuantileRange; // this is actually the outliers
          const max = q3 + 1.5 * interQuantileRange; // outliers
          return {
            q1: q1,
            median: median,
            q3: q3,
            interQuantileRange: interQuantileRange,
            min: min,
            max: max
          };
        })
        .entries(this.tableData);

      // Show the X scale
      const x = d3
        .scaleBand()
        .range([0, this.width])
        .domain(this.tableData.map(d => d.stain))
        .paddingInner(1)
        .paddingOuter(0.5);
      svg
        .append("g")
        .attr("transform", "translate(0," + this.height + ")")
        .style("font-size", "12px")
        .call(d3.axisBottom(x))
        .selectAll("text")
        .style("text-anchor", "end")
        .attr("transform", "rotate(-45)")
        .on("mouseover", function(d, i) {
          d3.select(this)
            .style("text-decoration", "underline")
            .style("cursor", "pointer");
        })
        .on("mouseout", function(d, i) {
          d3.select(this).style("text-decoration", "none");
        })
        .on("click", function(d, i) {
          console.log(d);
        });
      // Show the Y scale
      const y = d3
        .scaleLinear()
        .domain([-3, 4.5])
        .range([this.height, 0]);
      svg
        .append("g")
        .style("font-size", "12px")
        .call(d3.axisLeft(y));

      // Show the main vertical line
      svg
        .selectAll("vertLines")
        .data(sumstat)
        .enter()
        .append("line")
        .attr("x1", function(d) {
          return x(d.key);
        })
        .attr("x2", function(d) {
          return x(d.key);
        })
        .attr("y1", function(d) {
          return y(d.value.min);
        })
        .attr("y2", function(d) {
          return y(d.value.max);
        })
        .attr("stroke", "black");

      const heatColor = d3.interpolateRdBu;
      const myColor = d3
        .scaleSequential()
        .interpolator(heatColor)
        .domain([3, -3]);
      // rectangle for the main box
      const boxWidth = 22;
      svg
        .selectAll("boxes")
        .data(sumstat)
        .enter()
        .append("rect")
        .attr("x", function(d) {
          return x(d.key) - boxWidth / 2;
        })
        .attr("y", function(d) {
          return y(d.value.q3);
        })
        .attr("height", function(d) {
          return y(d.value.q1) - y(d.value.q3);
        })
        .attr("width", boxWidth)
        .attr("stroke", "black")
        .style("rx", "2px")
        .style("fill", "black") // change to real color
        .style("opacity", 0.4);

      // Show the median
      svg
        .selectAll("medianLines")
        .data(sumstat)
        .enter()
        .append("line")
        .attr("x1", function(d) {
          return x(d.key) - boxWidth / 2;
        })
        .attr("x2", function(d) {
          return x(d.key) + boxWidth / 2;
        })
        .attr("y1", function(d) {
          return y(d.value.median);
        })
        .attr("y2", function(d) {
          return y(d.value.median);
        })
        .attr("stroke", "black")
        .style("width", 80);

      // Add individual points with jitter
      const jitterWidth = 10;
      svg
        .selectAll("indPoints")
        .data(this.tableData)
        .enter()
        .append("circle")
        .attr("cx", function(d) {
          return x(d.stain) - jitterWidth / 2 + Math.random() * jitterWidth;
        })
        .attr("cy", function(d) {
          return y(d.value);
        })
        .attr("r", 3)
        .attr("fill", function(d) {
          return myColor(d.value);
        })
        .attr("stroke", "black")
        .on("mouseover", function(d, i) {
          d3.select(this)
            .attr("fill", "lime")
            .style("cursor", "pointer");
          tooltip.style("opacity", 1);
          d3.select(this)
            .style("stroke", "black")
            .html("value: " + d.value)
            .style("top", d3.mouse(d3.event.pageY) + "px");
        })
        .on("mousemove", function(d) {
          tooltip
            .html(`value: ${d.value} -- slideId: ${d.slide_id}`)
            .style("left", `${d3.mouse(d3.event.pageX) + 70}px`)
            .style("top", d3.mouse(d3.event.pageY) + "px");
        })
        .on("mouseout", function(d, i) {
          tooltip.style("opacity", 0);
          d3.select(this).attr("fill", function(d) {
            return myColor(d.value);
          });
        });

      // create a tooltip
      const tooltip = d3
        .select("#boxplot")
        .append("div")
        .style("opacity", 0)
        .attr("width", "100%")
        .attr("class", "tooltip")
        .style("background-color", "white")
        .style("border", "solid")
        .style("border-width", "2px")
        .style("border-radius", "5px")
        .style("padding", "5px");
    }
  }
};
</script>

<style scoped>
.hello {
  width: 100%;
}

.legend {
  width: 100%;
  height: 100%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
