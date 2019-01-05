<head>
  
</head>
<template>
   <div class="app align-items-center">
      <b-nav pills class="navbar">
      <b-navbar-brand class="navbar-brand" to="../About"></b-navbar-brand>
      <b-nav-item class="px-0" to="../About" style="border-radius:5px 5px 0 0">About</b-nav-item>
      <b-nav-item class="px-0" to="../News">News</b-nav-item>
      <b-nav-item class="px-0" active to="../ConfigMaker">Config maker<br>(PROTOTYPE)</b-nav-item>
      <b-nav-item class="px-0"  to="../IMonitor">IoT monitoring</b-nav-item>
    </b-nav>
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-2">
          <div class="card p-2">
                <b-btn v-b-toggle.collapse1 variant="primary">Target system --></b-btn>
                <b-collapse id="collapse1" class="mt-2">
                  <ul style="list-style-type:none">
                    <li><b-btn v-b-toggle.collapse1_inner size="sm" variant="success" v-on:click="ChangeTarget('#0000FF','ath25')">Atheros AR231x/AR5312</b-btn></li>
                    <li><b-btn v-b-toggle.collapse1_inner size="sm" variant="success" v-on:click="ChangeTarget('#00FF00','ar71xx')">Atheros AR7xxx/AR9xxx</b-btn></li>
                    </ul>
                </b-collapse><br>
                <b-btn v-b-toggle.collapse2 variant="primary">Subtarget --></b-btn>
                <b-collapse id="collapse2" class="mt-2">
                  <ul style="list-style-type:none">
                  <li><b-btn v-b-toggle.collapse2_inner size="sm" variant="success" v-on:click="ChangeSubtarget([1,1,1],'_generic')">Default Profile</b-btn></li>
                  <li><b-btn v-b-toggle.collapse2_inner size="sm" variant="success" v-on:click="ChangeSubtarget([0.8,0.8,0.8],'_tiny')">Devices with small flash</b-btn></li>
                  <li><b-btn v-b-toggle.collapse2_inner size="sm" variant="success" v-on:click="ChangeSubtarget([1.2,1.2,1.2],'_nand')">Generic devices with NAND flash</b-btn></li>
                  </ul>
                </b-collapse><br>
                <b-btn v-b-toggle.collapse3 variant="primary">Base system --></b-btn>
                <b-collapse id="collapse3" class="mt-2">
                  <ul style="list-style-type:none">
                  <li>base-files: 
                  <b-button-group>
                  <b-btn v-b-toggle.collapse3_inner size="sm" variant="success" v-b-tooltip.hover title="Auto" v-on:click="ChangeComponents('base-files', 'auto')">A</b-btn>
                  <b-btn v-b-toggle.collapse3_inner size="sm" variant="warning" v-b-tooltip.hover title="Manual" v-on:click="ChangeComponents('base-files', 'manual')">M</b-btn>
                  <b-btn v-b-toggle.collapse3_inner size="sm" variant="danger" v-b-tooltip.hover title="None" v-on:click="ChangeComponents('base-files', 'none')">N</b-btn>
                  </b-button-group>
                  </li>
                  
                  <li>busybox: 
                    <b-button-group>
                  <b-btn v-b-toggle.collapse4_inner size="sm" variant="success" v-b-tooltip.hover title="Auto" v-on:click="ChangeComponents('busybox', 'auto')">A</b-btn>
                  <b-btn v-b-toggle.collapse4_inner size="sm" variant="warning" v-b-tooltip.hover title="Manual" v-on:click="ChangeComponents('busybox', 'manual')">M</b-btn>
                  <b-btn v-b-toggle.collapse4_inner size="sm" variant="danger" v-b-tooltip.hover title="None" v-on:click="ChangeComponents('busybox', 'none')">N</b-btn>
                  </b-button-group>
                  </li>
                  <li>dns-masq:
                    <b-button-group>
                  <b-btn v-b-toggle.collapse5_inner size="sm" variant="success" v-b-tooltip.hover title="Auto" v-on:click="ChangeComponents('dns-masq', 'auto')">A</b-btn>
                  <b-btn v-b-toggle.collapse5_inner size="sm" variant="warning" v-b-tooltip.hover title="Manual" v-on:click="ChangeComponents('dns-masq', 'manual')">M</b-btn>
                  <b-btn v-b-toggle.collapse5_inner size="sm" variant="danger" v-b-tooltip.hover title="None" v-on:click="ChangeComponents('dns-masq', 'none')">N</b-btn>
                  </b-button-group>
                  </li>
                  <li>dropbear:
                    <b-button-group>
                  <b-btn v-b-toggle.collapse6_inner size="sm" variant="success" v-b-tooltip.hover title="Auto" v-on:click="ChangeComponents('dropbear', 'auto')">A</b-btn>
                  <b-btn v-b-toggle.collapse6_inner size="sm" variant="warning" v-b-tooltip.hover title="Manual" v-on:click="ChangeComponents('dropbear', 'manual')">M</b-btn>
                  <b-btn v-b-toggle.collapse6_inner size="sm" variant="danger" v-b-tooltip.hover title="None" v-on:click="ChangeComponents('dropbear', 'none')">N</b-btn>
                  </b-button-group>
                  </li>
                  <li>firewall:
                    <b-button-group>
                  <b-btn v-b-toggle.collapse7_inner size="sm" variant="success" v-b-tooltip.hover title="Auto" v-on:click="ChangeComponents('firewall', 'auto')">A</b-btn>
                  <b-btn v-b-toggle.collapse7_inner size="sm" variant="warning" v-b-tooltip.hover title="Manual" v-on:click="ChangeComponents('firewall', 'manual')">M</b-btn>
                  <b-btn v-b-toggle.collapse7_inner size="sm" variant="danger" v-b-tooltip.hover title="None" v-on:click="ChangeComponents('firewall', 'none')">N</b-btn>
                  </b-button-group>
                  </li>
                  </ul>
                </b-collapse>
        </div>
        </div>
        <div class="col-md-10">

            <div class="card p-10">
                      <Scene :fog="none">
                      
                        <Entity>
                          <Camera :position="[0, -3.5, 7]">
                          
                          <IcoSphere :position="[0, 3, 0]" v-bind:scaling="this.CoreSize">
                            <Material v-bind:diffuse="this.CoreColor"></Material>
                          </IcoSphere>

                          <Box :position="[2, 3, 2]" >
                            <Material v-bind:alpha="this.Packages[0].status" v-bind:diffuse="this.Packages[0].color"></Material>
                          </Box>
                          <Box :position="[-2, 3, -2]" ><Material v-bind:alpha="this.Packages[1].status" v-bind:diffuse="this.Packages[1].color"></Material></Box>
                          <Box :position="[2, 3, -2]" ><Material v-bind:alpha="this.Packages[2].status" v-bind:diffuse="this.Packages[2].color"></Material></Box>
                          <Box :position="[-2, 3, 2]" ><Material v-bind:alpha="this.Packages[3].status" v-bind:diffuse="this.Packages[3].color"></Material></Box>

                          <Box :position="[2, 3, 0]" ></Box>
                          <Box :position="[0, 3, 2]" ></Box>
                          <Box :position="[0, 3, -2]" ></Box>
                          <Box :position="[-2, 3, 0]" ></Box>

                          <Box :position="[-2, 1, -2]" ></Box>
                          <Box :position="[2, 1, -2]" ></Box>
                          <Box :position="[-2, 1, 2]" ></Box>
                          <Box :position="[2, 1, 2]" ></Box>
                          <Box :position="[2, 1, 0]" ></Box>
                          <Box :position="[0, 1, 2]" ></Box>
                          <Box :position="[0, 1, -2]" ></Box>
                          <Box :position="[-2, 1, 0]" ></Box>
                          <Box :position="[0, 1, 0]" ><Material v-bind:alpha="this.Packages[4].status" v-bind:diffuse="this.Packages[4].color"></Material></Box>

                          <Box :position="[-2, 5, -2]" ></Box>
                          <Box :position="[2, 5, -2]" ></Box>
                          <Box :position="[-2, 5, 2]" ></Box>
                          <Box :position="[2, 5, 2]" ></Box>
                           <Box :position="[0, 5, -2]" ></Box>
                          <Box :position="[0, 5, 2]" ></Box>
                          <Box :position="[-2, 5, 0]" ></Box>
                          <Box :position="[0, 5, 0]" ></Box>
                          <Box :position="[2, 5, 0]" ></Box>

                              <Animation property="rotation.y" :duration="25">
                                  <Key frame="0%" :value="0"></Key>
                                  <Key frame="100%" :value="Math.PI * 2"></Key>
                              </Animation>
                              <Animation property="rotation.y" :duration="125" :end="Math.PI * 2"></Animation>
                              <PointLight diffuse="#FF0000"></PointLight>
                        </Camera>
                        </Entity>
                      </Scene>
            </div>

        </div>
        <div class="col-md-12">
          <div class="card p-12">
                <b-form>
                  <b-form-textarea
                     v-model="this.OutputConfig"
                     placeholder="Config file"
                     :rows="5"
                     :max-rows="100">
                  </b-form-textarea><br>
                </b-form>
                <center><form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top">
                <input type="hidden" name="cmd" value="_s-xclick">
                <input type="hidden" name="hosted_button_id" value="6WQA8E4M4PJXY">
                <input type="image" src="https://www.paypalobjects.com/en_US/GB/i/btn/btn_donateCC_LG.gif" border="0" name="submit" alt="PayPal – The safer, easier way to pay online!">
                <img alt="" border="0" src="https://www.paypalobjects.com/ru_RU/i/scr/pixel.gif" width="1" height="1">
                </form></center>
          </div>
        </div>
      </div>
      </div>
  </div>
</template>


<script>
export default {
  name: 'ConfigMaker',
  data: function () {
    return {
      CoreColor: '#FF0000',
      Platform: '',
      Subtarget: '',
      CoreSize: [1, 1, 1],
      OutputConfig: '',
      Packages: [
        { name: 'base-files',
          status: 1,
          color: '#FF00FF'
        },
        { name: 'busybox',
          status: 1,
          color: '#FF00FF'
        },
        { name: 'dns-masq',
          status: 1,
          color: '#FF00FF'
        },
        { name: 'dropbear',
          status: 1,
          color: '#FF00FF'
        },
        { name: 'firewall',
          status: 1,
          color: '#FF00FF'
        }
      ]
    }
  },
  created: function () {
    // console.log('created')
    // window.location.resize()
  },
  methods: {
    ChangeTarget (CoreColor, Platform) {
      this.CoreColor = CoreColor
      this.Platform = Platform
      this.MakeConfig()
    },
    ChangeSubtarget (Size, Subtarget) {
      this.CoreSize = Size
      this.Subtarget = Subtarget
      this.MakeConfig()
    },
    MakeConfig () {
      this.OutputConfig = ''
      var t = ''
      t = t + 'CONFIG_MODULES=y \n'
      t = t + 'CONFIG_HAVE_DOT_CONFIG=y \n'
      t = t + 'CONFIG_TARGET_' + this.Platform + '=y\n'
      t = t + 'CONFIG_TARGET_' + this.Platform + this.Subtarget + '=y\n'
      if (this.Packages[0].status === 1) {
        t = t + 'CONFIG_PACKAGE_base-files=y \n'
      }
      if (this.Packages[1].status === 1) {
        t = t + 'CONFIG_PACKAGE_busybox=y \n'
      }
      if (this.Packages[2].status === 1) {
        t = t + 'CONFIG_PACKAGE_dns-masq=y \n'
      }
      if (this.Packages[3].status === 1) {
        t = t + 'CONFIG_PACKAGE_dropbear=y \n'
      }
      if (this.Packages[4].status === 1) {
        t = t + 'CONFIG_PACKAGE_firewall=y \n'
      }
      this.OutputConfig = t
    },
    ChangeComponents (name, status) {
      for (var i in this.Packages) {
        if (this.Packages[i].name === name) {
          if (status === 'auto') {
            this.Packages[i].status = 1
            this.Packages[i].color = '#FF00FF'
          } else if (status === 'manual') {
            this.Packages[i].status = 0.2
            this.Packages[i].color = '#0000FF'
          } else if (status === 'none') {
            this.Packages[i].status = 0
          }
        }
      }
      this.MakeConfig()
      // console.log(this.Packages)
    }

  }
}
</script>
