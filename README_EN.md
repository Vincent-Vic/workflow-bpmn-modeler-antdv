English | [įŽäŊä¸­æ](./README.md) | [GitHub](https://github.com/Vincent-Vic/workflow-bpmn-modeler-antdv) | [Gitee](https://gitee.com/Vincent-Vic/workflow-bpmn-modeler-antdv)

# workflow-bpmn-modeler

[![NPM Version](http://img.shields.io/npm/v/workflow-bpmn-modeler.svg?style=flat)](https://www.npmjs.org/package/workflow-bpmn-modeler)
[![NPM Downloads](https://img.shields.io/npm/dm/workflow-bpmn-modeler.svg?style=flat)](https://www.npmjs.org/package/workflow-bpmn-modeler)
![](https://img.shields.io/badge/license-MIT-000000.svg)

đĨ This project implements flowable's workflow designer based on `vue` and `bpmn.io@7.0`

## Preview đ

![1.0.2](https://cdn.jsdelivr.net/gh/Vincent-Vic/image@master/workflow-bpmn-modeler-antdv/1.0.2.png)

## Online demo đĸ

đ https://vincent-vic.github.io/workflow-bpmn-modeler-antdv/demo/

## Install âŗ

```bash
# yarn
yarn add workflow-bpmn-modeler-antdv
# Or npm
npm i workflow-bpmn-modeler-antdv
```

## How to use đŖ
#### simple demo
```vue
<template>
  <div>
    <bpmn-modeler
      ref="refNode"
      :xml="xml"
      :users="users"
      :groups="groups"
      :categorys="categorys"
      :is-view="false"
      @save="save"
    />
  </div>
</template>

<script>
import bpmnModeler from "workflow-bpmn-modeler";

export default {
  components: {
    bpmnModeler,
  },
  data() {
    return {
      xml: "", // Query the xml
      users: [
        { name: "The Beatles", id: "1" },
        { name: "The Rolling Stones", id: "2" },
        { name: "Pink Floyed", id: "3" },
      ],
      groups: [
        { name: "Folk Music", id: "4" },
        { name: "Rock Music", id: "5" },
        { name: "Classical Music", id: "6" },
      ],
      categorys: [
        { name: "Music", id: "7" },
        { name: "Articles", id: "8" },
      ],
    };
  },
  methods: {
    getModelDetail() {
      // Send request to get xml
      // this.xml = response.xml
    },
    save(data) {
      console.log(data);  // { process: {...}, xml: '...', svg: '...' }
    },
  },
};
</script>
```

#### Full demo
```vue
<template>
  <div id="app">
    <bpmn-modeler
        ref="refNode"
        :xml="xml"
        :users="users"
        :groups="groups"
        :categories="categories"
        :is-view="false"

        :paletteToolShow="paletteToolShow"
        :panelFilters="panelFilters"
        :paletteFilters="paletteFilters"
        :show-initiator="showInitiator"
        :initiator="initiator"
        :associate-form-config="associateFormConfig"
        :associate-form-data-options="associateFormDataOptions"
        :assignee-data-source="assigneeDataSource"
        :due-date-data-source="dueDateDataSource"
        :follow-up-date-data-source="followUpDateDataSource"
        :initiator-data-source="initiatorDataSource"
        :skip-expression-data-source="skipExpressionDataSource"
        :condition-expression-data-source="conditionExpressionDataSource"
        @save="saveModeler"
        @showForm="showAssociateForm"
        @createForm="createAssociateForm"
    >
      <!--åˇĻčžšæŠåąæéŽį¤ēäž-->
      <div slot="header-left">
        <a-button>åˇĻčžšæŠåą</a-button>
      </div>
      <!--åŗčžšæŠåąæéŽį¤ēäž-->
      <div slot="header-right">
        <a-button>åŗčžšæŠåą</a-button>
      </div>
    </bpmn-modeler>

    <a-modal v-model:visible="formShowVisible" title="æžį¤ēčĄ¨å" width="400px">
      <template #footer>
      </template>
      ãæžį¤ēčĄ¨åãæŦåčŊä¸ēå¤é¨æŠåąīŧéįģäģļåé¨åŧšįĒ,į¨äēæĨåĨflowableå¨æčĄ¨åæåļäģčĒåŽäšå¨æčĄ¨å....
    </a-modal>
    <a-modal v-model:visible="formCreateVisible" title="ååģēčĄ¨å" width="400px">
      <template #footer>
      </template>
      ãååģēčĄ¨åãæŦåčŊä¸ēå¤é¨æŠåąīŧéįģäģļåé¨åŧšįĒ,į¨äēæĨåĨflowableå¨æčĄ¨åæåļäģčĒåŽäšå¨æčĄ¨å....
    </a-modal>
  </div>
</template>

<script>
import bpmnModeler from '../package/index'

export default {
  components: {
    bpmnModeler
  },
  data() {
    return {
      xml: '', // åįĢ¯æĨč¯ĸå°įxml
      users: [
        { name: 'åŧ ä¸', id: 'zhangsan' },
        { name: 'æå', id: 'lisi' },
        { name: 'įäē', id: 'wangwu' }
      ],
      groups: [
        { name: 'webįģ', id: 'web' },
        { name: 'javaįģ', id: 'java' },
        { name: 'pythonįģ', id: 'python' }
      ],
      categories: [
        { name: 'OA', id: 'oa' },
        { name: 'č´ĸåĄ', id: 'finance' }
      ],
      //čŋæģ¤éĸæŋåæ°īŧåæ°č§ææĄŖ
      panelFilters: [],
      //panelFilters: ['category','message'],
      //įģäģļæ čŋæģ¤īŧčŋæģ¤åæ°č§ææĄŖ
      //paletteFilters:['space-tool','create.start-event','create.task'],
      paletteFilters:[],
      paletteToolShow:true,//čŽžįŊŽfalseįģäģļįæäŊæ å°čĸĢéč
      rightActionConfig: {
        'showCode': {
          'show': true,
          'icon': true,
          'label': 'XML'
        },
        'downloadXML': {
          'show': true,
          'icon': true,
          'label': 'XML'
        },
        'downloadSVG': {
          'show': true,
          'icon': true,
          'label': 'SVG'
        },
        'save': {
          'show': true,
          'icon': true,
          'label': 'äŋå­'
        }
      },
      showInitiator:true,
      initiator:{
        label: "æĩį¨åčĩˇäēē",
        value: "${INITIATOR}"
      },
      associateFormConfig:{
        enable:true, //æ­¤éĄšä¸ēfalseīŧåčŽžįŊŽä¸¤éĄšåæ æ
        isPreview: true,
        isCreate: true,
      },
      associateFormDataOptions: [],
      assigneeDataSource: ["#{approval}","${approverId}","${INITIATOR}"],
      dueDateDataSource:  ["${dueDate}"],
      followUpDateDataSource: ["${followUpDate}"],
      initiatorDataSource: ["initiator"],
      skipExpressionDataSource: [],
      conditionExpressionDataSource: ['${approve}','${!approve}'],

      //åŗččĄ¨åæŠåąīŧį¨äēæĨåĨflowableå¨æčĄ¨åæåļäģčĒåŽäšå¨æčĄ¨å
      formShowVisible: false,
      formCreateVisible:false
    }
  },
  mounted() {
    this.getModelDetail()
  },
  methods: {
    getModelDetail() {
      fetch('https://cdn.jsdelivr.net/gh/Vincent-Vic/workflow-bpmn-modeler-antdv@master/src/Leave.bpmn20.xml')
          .then(response => {
            return response.text()
          }).then(xml => {
        this.xml = xml
      })
    },
    saveModeler(data) {
      console.log(data)
    },
    showAssociateForm(formKey){
      console.log(formKey)
      this.formShowVisible = true;
    },
    createAssociateForm(){
      console.log("create form")
      this.formCreateVisible = true;
    }
  }
}
</script>

<style lang="scss">
html, body, #app {
  height: 100%;
  margin: 0;
}
</style>

```
## Props
### Primary Props


| Attributes        | describe                        | structure                                                    | type    | default |
| ----------------- | ------------------------------- | ------------------------------------------------------------ | ------- | ------- |
| xml               | xml                             |                                                              | String  | ''      |
| users             | assignee or candidate user list | [<br/>  { name: 'name', id: 'id' },<br/>]                    | Array   | []      |
| groups            | candidate groups                | [<br/>    { name: 'name', id: 'id' },<br/>]                  | Array   | []      |
| categories        | process categories              | [<br/>    { name: 'name', id: 'id' },<br/>]                  | Array   | []      |
| isView            | class view-mode                 |                                                              | Boolean | false   |
| rightActionConfig | head right action config        | {<br/>  ".*":{<br/>    "show":true,<br/>    "icon":true,<br/>    "label":"XML"<br/>    }<br/>  } | Object  | č§ä¸æ  |

rightActionConfig default

```json
{
  "showCode":{
    "show":true,
    "icon":true,
    "label":"XML"
  },
  "downloadXML":{
    "show":true,
    "icon":true,
    "label":"XML"
  },
  "downloadSVG":{
    "show":true,
    "icon":true,
    "label":"SVG"
  },
  "save":{
    "show":true,
    "icon":true,
    "label":"äŋå­"
  }
}
```

### Panel Props

| Attributes                    | describe                                      | type    | default                                                      |
| ----------------------------- | --------------------------------------------- | ------- | ------------------------------------------------------------ |
| filters                       | panel filter attributes                       | Array   | []                                                           |
| showInitiator                 | Whether the initiator is displayed in the assignee (fixed mode) | Boolean | true                                                         |
| initiator                     | assignee display content | Object  | {<br/>    label: "æĩį¨åčĩˇäēē",<br/>    value: "${INITIATOR}"<br/>} |
| associateFormConfig           | associate form config                         | Object  | {<br/>//æ­¤éĄšä¸ēfalseīŧåčŽžįŊŽä¸¤éĄšåæ æ<br/>    enable:false,  <br/>   isView: true,<br/>    isCreate: true,<br/>} |
| associateFormDataOptions      | associate form auto complete dataSource       | Array   |                                                              |
| assigneeDataSource            | assignee auto complete dataSource             | Array   | [<br/>    "#{approval}",<br/>    "${approverId}",<br/>    "${INITIATOR}"<br/>] |
| dueDateDataSource             | due date auto complete dataSource             | Array   | ["${dueDate}"]                                               |
| followUpDateDataSource        | follow up auto complete dataSource            | Array   | ["${followUpDate}"]                                          |
| initiatorDataSource           | initiator auto complete dataSource            | Array   | ["initiator"]                                                |
| skipExpressionDataSource      | skip expression auto complete dataSource      | Array   | []                                                           |
| conditionExpressionDataSource | condition expression auto complete dataSource | Array   | []                                                           |




#### panel filtering
```javascript
panelFilters: {
  type: Array,
  default: () => []
}
```
Parameter List

| ééĄš              | čŋæģ¤å­æŽĩ            |
| ----------------- | ------------------- |
| æĩį¨åįąģ          | category            |
| æĩį¨æčŋ°          | documentation       |
| æ§čĄįåŦå¨        | executionListener   |
| äŋĄåˇåŽäš          | signal              |
| æļæ¯åŽäš          | message             |
| čįšæčŋ°          | nodeDocumentation   |
| čˇŗčŊŦæĄäģļ          | conditionExpression |
| čˇŗčŋæĄäģļ          | skipExpression      |
| åčĩˇäēē            | initiator           |
| čĄ¨åæ č¯/čĄ¨åæčŊŊ | formKey             |
| äģģåĄįåŦå¨        | taskListener        |
| å¤åŽäž            | multiInstance       |
| åŧæ­Ĩ              | async               |
| äŧåįē§            | priority            |
| æ¯åĻä¸ēčĄĨåŋ        | isForCompensation   |
| æåĄäģģåĄå¯č§Ļå    | triggerable         |
| čĒå¨å­å¨åé      | autoStoreVariables  |
| æé¤              | exclude             |
| čžåĨåé          | ruleVariablesInput  |
| č§å              | rules               |
| įģæåé          | resultVariable      |
| įąģ                | class               |
| čŋææļé´          | dueDate             |
| č§å¯æļé´          | followUpDate        |

### palette đŖ
#### palette filtering đŖ
paletteFilters čŽžįŊŽå¯äģĨå°æäŊæ įģäģļéč
| ééĄš     | čŋæģ¤å­æŽĩ                    |
| -------- | --------------------------- |
| ææ     | hand-tool                   |
| åĨį´ĸ     | lasso-tool                  |
| įŠēé´     | space-tool                  |
| čŋæĨ     | global-connect-tool         |
| åŧå§     | create.start-event          |
| ä¸­é´     | create.intermediate-event   |
| įģæ     | create.end-event            |
| įŊåŗ     | create.exclusive-gateway    |
| äģģåĄ     | create.task                 |
| å­æĩį¨   | create.subprocess-expanded  |
| æ°æŽå¯ščąĄ | create.data-object          |
| æ°æŽå­å¨ | create.data-store           |
| æŠåąå­å¨ | create.participant-expanded |
| åįģ     | create.group                |


## Iframe Deployment đĒ

If your project is a `jquery` or `react` project, you can integrate the workflow designer by means of an iframe

This repository deployed a static page by the github pages, using `jsdelivr` cdn, access in China is also very fast, so you can directly integrate the pages of this repository, because all the free github resources are used, did not build their own server maintenance, so do not worry about the failure of resources.

Of course you can also download the corresponding version from the `docs/lib` folder for local deployment.

The integration method is as follows (ps: you can copy the following code directly into an html file and try it out)

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <iframe
      src="https://vincent-vic.github.io/workflow-bpmn-modeler-antdv/cdn/1.0.1/"
      id="myFrame"
      frameborder="0"
      width="100%"
      height="800px">
    </iframe>

    <script>
      let myFrame = document.getElementById("myFrame");
      // Get details
      window.addEventListener("message", (event) => {
        console.log(event.data); // { xml: 'xxx', img: 'xxx', process: {} }
      });
      myFrame.onload = () => {
        let postMsg = {
          xml: "", // Query the xml
          users: [
            { name: "The Beatles", id: "1" },
            { name: "The Rolling Stones", id: "2" },
            { name: "Pink Floyed", id: "3" },
          ],
          groups: [
            { name: "Folk Music", id: "4" },
            { name: "Rock Music", id: "5" },
            { name: "Classical Music", id: "6" },
          ],
          categorys: [
            { name: "Music", id: "7" },
            { name: "Articles", id: "8" },
          ],
          isView: false
        }
        // Set initialization value
        myFrame.contentWindow.postMessage(postMsg, "*")
      }
    </script>
  </body>
</html>
```

## Customization đ 

This component is aligned to the official flowable designer, which is the standard for implementing flowable's xml rules, and the terms used in it are all terminology from the official documentation. So this component is just a tool for programmers to model and export xml by themselves during the development phase, and it is wrong to try to customize the behavior of this modeler. Your own business should be developed separately to implement it.

The component will not upgrade the UI library or vue in the future, and regardless of library compatibility, integrating the modeler via an iframe is the easiest and correct way to do it.

## Sponsor đ§Ą


## License đ

[MIT](http://opensource.org/licenses/MIT)

base Copyright (c) 2020-present, charles

Copyright (c) 2022-present, Vincent-Vic
