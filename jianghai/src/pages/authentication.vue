<template>
	<div class="authentication">
		<header class="navbar-fixed-top headerBg">
			<nav class="navbar navbar-default bootsnav on no-full">
				<div class="container">
					<div class="navbar-header">
						<router-link to="/test">
							<div class="logo">
								<img src="../../static/images/logo.png" class="img-responsive">
							</div>
						</router-link>
					</div>
					<router-link to="/index">
						<div class="back">
							返回首页
						</div>
					</router-link>
				</div>
			</nav>
		</header>
		<div class="container" style="min-height: 1000px;">
			<div class="information">
				<div class="user">
					<img src="../../static/images/userIcon.png" />
					<p>用户{{Phone}}，您好！</p>
				</div>
				<h2>{{UserType}}</h2><span>认证资料上报</span>
			</div>
			<el-form :inline="true" :rules="rules" ref="form" :model="form">
				<!--基本信息-->
				<div class="inforTitle">
					<h2>基本信息</h2>
				</div>
				<h3>注册信息</h3>
				<div class="form-box basic width110">
					<el-form-item prop="name" label="姓名">
						<el-input v-model="form.name" placeholder="请输入姓名"></el-input>
					</el-form-item>
					<el-form-item prop="cellphone" label="手机">
						<el-input v-model.number="form.cellphone" placeholder="请输入手机号"></el-input>
					</el-form-item>
					<el-form-item prop="gender" label="性别">
						<el-input v-model="form.gender" placeholder="请输入性别"></el-input>
					</el-form-item>
					<el-form-item prop="Wechat" label="微信号">
						<el-input v-model="form.Wechat" placeholder="请输入微信号"></el-input>
					</el-form-item>
					<el-form-item prop="nationality" label="国籍">
						<el-input v-model="form.nationality" placeholder="请输入国籍"></el-input>
					</el-form-item>
					<el-form-item prop="email" label="邮箱">
						<el-input v-model="form.email" placeholder="请输入邮箱"></el-input>
					</el-form-item>
					<el-form-item prop="nation" label="民族">
						<el-input v-model="form.nation" placeholder="请输入民族"></el-input>
					</el-form-item>
					<el-form-item prop="idType" label="证件类型">
						<el-select v-model="form.idType" placeholder="请选择证件类型">
							<el-option label="身份证" value="0"></el-option>
							<el-option label="签证" value="1"></el-option>
							<el-option label="护照" value="2"></el-option>
						</el-select>
					</el-form-item>
					<el-form-item prop="maritalStatus" label="婚姻状况">
						<el-input v-model="form.maritalStatus" placeholder="请输入婚姻状况"></el-input>
					</el-form-item>
					<el-form-item prop="idTypeNumber" label="证件号">
						<el-input v-model="form.idTypeNumber" placeholder="请输入证件号"></el-input>
					</el-form-item>
				</div>
				<h3>教育信息</h3>
				<div class="form-box width80">
					<el-form-item label="最高学历" class="hiEducation width110" prop="education" align="center" style="width:1000px">
						<el-radio-group v-model="form.education">
							<el-radio label="博士"></el-radio>
							<el-radio label="硕士"></el-radio>
							<el-radio label="学士"></el-radio>
							<el-radio label="高中"></el-radio>
						</el-radio-group>
					</el-form-item>
					<el-form-item prop="school" label="学校">
						<el-input v-model="form.school" placeholder="请输入学校"></el-input>
					</el-form-item>
					<el-form-item prop="professional" label="专业">
						<el-input v-model="form.professional" placeholder="请输入专业"></el-input>
					</el-form-item>
					<el-form-item prop="graduationDate" label="毕业时间">
						<el-date-picker v-model="form.graduationDate" type="year" placeholder="选择日期">
						</el-date-picker>
					</el-form-item>
				</div>
				<h3>工作信息</h3>
				<div class="form-box basic width110 border-bottom">
					<el-form-item prop="work" label="单位">
						<el-input v-model="form.work" placeholder="请输入单位名称"></el-input>
					</el-form-item>
					<el-form-item prop="duty" label="职务">
						<el-input v-model="form.duty" placeholder="请输入职务"></el-input>
					</el-form-item>
					<el-form-item prop="rank" label="职级">
						<el-select v-model="form.rank" placeholder="请选择职级">
							<el-option label="高管" value="0"></el-option>
							<el-option label="实际控制人" value="1"></el-option>
						</el-select>
					</el-form-item>
					<el-form-item prop="city" label="所在地区 ">
						<el-input v-model="form.city" placeholder="请输入所在地区"></el-input>
					</el-form-item>
					<el-form-item prop="workbackground" label="工作经历 ">
						<el-input type="textarea" v-model="form.workbackground" placeholder="请输入工作经历"></el-input>
					</el-form-item>
				</div>
				<!--特征信息-->
				<div class="inforTitle">
					<h2>特征信息</h2>
				</div>
				<!--如果角色选择为创业者，则显示-->
				<div class="ESTP" v-show="ESTP">
					<h3>创业履历</h3>
					<div class="form-box basic width130">
						<el-form-item label="是否为首次创业" prop="firstBusiness">
							<el-radio-group v-model="form.firstBusiness" style="width: 120px;">
								<el-radio label="0">是</el-radio>
								<el-radio label="1">否</el-radio>
							</el-radio-group>
						</el-form-item>
						<el-form-item v-show="form.firstBusiness==0" label="创业经历与成果 " prop="achievement">
							<el-input type="textarea" v-model="form.achievement" placeholder="请输入创业经历与成果"></el-input>
						</el-form-item>
						<el-form-item label="工作经历 " prop="businessbackground">
							<el-input type="textarea" v-model="form.businessbackground" placeholder="请输入工作经历，如没有，填写“无”。"></el-input>
						</el-form-item>
					</div>
					<h3>当前创业情况</h3>
					<div class="form-box basic">
						<el-form-item label="创业领域" prop="entrepreneurship">
							<el-select v-model="form.entrepreneurship" placeholder="请选择创业领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
							<!--<el-input v-if="form.entrepreneurship==9" placeholder="请填写其它领域"></el-input>-->
						</el-form-item>
						<el-form-item label="创业目标 " prop="AnnualRevenue" class="reset-input">
							<div class="target">
								每年营收：
								<el-input v-model="form.AnnualRevenue" placeholder=""></el-input><span>万元</span>
							</div>
							<div class="target">
								融资规模：
								<el-input v-model="form.financingScale" placeholder=""></el-input><span>万元</span>
							</div>
							<div class="target">
								客户规模：
								<el-input v-model="form.customerSize" placeholder=""></el-input><span>人</span>
							</div>
							<div class="target">
								企业规模：
								<el-input v-model="form.scale" placeholder=""></el-input><span>人</span>
							</div>
							<div class="target">
								其他：
								<el-input v-model="form.targetElse" placeholder=""></el-input>
							</div>
						</el-form-item>
						<el-form-item label="创业项目概述 " prop="summarize">
							<el-input type="textarea" v-model="form.summarize" placeholder="请输入创业项目概述"></el-input>
						</el-form-item>
						<el-form-item label="创业性成果 " prop="CGAnnualRevenue" class="reset-input">
							<div class="target">
								每年营收：
								<el-input v-model="form.CGAnnualRevenue" placeholder=""></el-input><span>万元</span>
							</div>
							<div class="target">
								融资规模：
								<el-input v-model="form.CGfinancingScale" placeholder=""></el-input><span>万元</span>
							</div>
							<div class="target">
								客户规模：
								<el-input v-model="form.CGcustomerSize" placeholder=""></el-input><span>人</span>
							</div>
						</el-form-item>
					</div>
					<h3>意见诉求</h3>
					<div class="form-box basic width110 border-bottom">
						<el-form-item label="资源需求" prop="resourceNeeds">
							<el-select v-model="form.resourceNeeds" placeholder="请选择资源需求">
								<el-option label="资金" value="0"></el-option>
								<el-option label="技术" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="人才" value="3"></el-option>
								<el-option label="孵化空间" value="4"></el-option>
								<el-option label="其它" value="5"></el-option>
							</el-select>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为投资人，则显示-->
				<div class="investor" v-show="investor">
					<!--<div class="form-box basic width130 border-bottom">
					<el-form-item label="个人金融资产" prop="financialAssets" style="width: 100%;">
						<el-select v-model="form.financialAssets" placeholder="请选择创业领域">
							<el-option label="300万及以上" value="0"></el-option>
							<el-option label="近三年年均收入50万以上" value="1"></el-option>
							<el-option label="其它" value="3"></el-option>
						</el-select>
						<el-input v-if="form.entrepreneurship==3" placeholder="请填写其它金融资产"></el-input>
					</el-form-item>
					<p>投资经历</p>
					<el-form-item class="multiInput" label="过往投资项目 " prop="PastInvestments">
						<el-input v-model="form.PastInvestments" placeholder="如没有，填写“无”。"></el-input>
					</el-form-item>
					<el-form-item class="multiInput" label="投后情况 " prop="CastConditionAfter">
						<el-input v-model="form.CastConditionAfter" placeholder="如没有，填写“无”。"></el-input>
					</el-form-item>
				</div>-->
					<h3>投资背景</h3>
					<div class="form-box basic width130">
						<el-form-item label="个人金融资产" prop="financialAssets" style="width: 100%;">
							<el-select v-model="form.financialAssets" placeholder="请选择创业领域">
								<el-option label="300万及以上" value="0"></el-option>
								<el-option label="近三年年均收入50万以上" value="1"></el-option>
								<el-option label="其它" value="3"></el-option>
							</el-select>
							<el-input v-if="form.entrepreneurship==3" placeholder="请输入其它金融资产"></el-input>
						</el-form-item>
					</div>
					<h3>投资经历</h3>
					<div class="form-box basic width130">
						<el-form-item prop="PastInvestments" label="过往投资项目">
							<el-input v-model="form.PastInvestments" placeholder="如没有，填写“无”"></el-input>
						</el-form-item>
						<el-form-item prop="CastConditionAfter" label="投后情况">
							<el-input v-model="form.CastConditionAfter" placeholder="如没有，填写“无”"></el-input>
						</el-form-item>
					</div>
					<h3>投资倾向</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="fieldInvestment" label="投资领域">
							<el-select v-model="form.fieldInvestment" placeholder="请选择投资领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="investmentStage" label="投资阶段">
							<el-input v-model="form.investmentStage" placeholder="请输入投资阶段"></el-input>
						</el-form-item>
						<el-form-item prop="investmentStage" label="投资阶段">
							<el-input v-model="form.investmentStage" placeholder="请输入投资阶段"></el-input>
						</el-form-item>
						<el-form-item label="其他喜好">
							<el-input v-model="form.otherPreferences" placeholder="请输入其他喜好"></el-input>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为FA机构，则显示-->
				<div class="FAInstitution" v-show="FAInstitution">
					<h3>业务</h3>
					<div class="form-box basic width130">
						<el-form-item prop="businessDirection" label="业务方向">
							<el-select v-model="form.businessDirection" placeholder="请选择业务方向">
								<el-option label="私募融资" value="0"></el-option>
								<el-option label="投资咨询" value="1"></el-option>
								<el-option label="创业咨询" value="2"></el-option>
								<el-option label="战略规划" value="3"></el-option>
								<el-option label="合并收购" value="4"></el-option>
								<el-option label="战略重组" value="5"></el-option>
								<el-option label="IPO" value="6"></el-option>
								<el-option label="定向增发" value="7"></el-option>
								<el-option label="其它" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="coveringDomain" label="覆盖领域">
							<el-select v-model="form.coveringDomain" placeholder="请选择覆盖领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="clientType" label="客户类型">
							<el-select v-model="form.clientType" placeholder="请选择客户类型">
								<el-option label="政府" value="0"></el-option>
								<el-option label="高校" value="1"></el-option>
								<el-option label="海外" value="2"></el-option>
								<el-option label="国企" value="3"></el-option>
								<el-option label="高新技术企业" value="4"></el-option>
								<el-option label="500强企业" value="5"></el-option>
								<el-option label="个人企业家" value="6"></el-option>
								<el-option label="其它" value="7"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="investmentStage" label="业务特色">
							<el-input v-model="form.investmentStage" placeholder="请输入业务特色"></el-input>
						</el-form-item>
						<el-form-item prop="onlinePlatform" label="有无线上对接平台">
							<el-radio-group v-model="form.onlinePlatform">
								<el-radio label="0">是</el-radio>
								<el-radio label="1">否</el-radio>
								<el-radio label="2">筹备中</el-radio>
							</el-radio-group>
						</el-form-item>
					</div>
					<h3>成果资质</h3>
					<div class="form-box basic width130">
						<el-form-item prop="typicalCase" label="典型案例">
							<el-input v-model="form.typicalCase" placeholder="请输入典型案例"></el-input>
						</el-form-item>
						<el-form-item prop="LicenceQualification" label="牌照资质">
							<el-input v-model="form.LicenceQualification" placeholder="请输入牌照资质"></el-input>
						</el-form-item>
						<el-form-item prop="partner" label="合作伙伴">
							<el-input v-model="form.partner" placeholder="请输入合作伙伴"></el-input>
						</el-form-item>
					</div>
					<h3>诉求调研</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="fundType" label="基金类型">
							<el-select v-model="form.fundType" placeholder="请选择基金类型">
								<el-option label="科创类" value="0"></el-option>
								<el-option label="产业类" value="1"></el-option>
								<el-option label="股权类" value="2"></el-option>
								<el-option label="天使类" value="3"></el-option>
								<el-option label="VC类" value="4"></el-option>
								<el-option label="并购类" value="5"></el-option>
								<el-option label="固收类" value="6"></el-option>
								<el-option label="配置型" value="7"></el-option>
								<el-option label="其它" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="FundPhase" label="基金阶段">
							<el-select v-model="form.FundPhase" placeholder="请选择基金阶段">
								<el-option label="天使" value="0"></el-option>
								<el-option label="VC" value="1"></el-option>
								<el-option label="PE" value="2"></el-option>
								<el-option label="一级半" value="3"></el-option>
								<el-option label="二级" value="4"></el-option>
								<el-option label="其他" value="5"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="businessDirection" label="业务发展方向">
							<el-select v-model="form.businessDirection" placeholder="请选择业务发展方向">
								<el-option label="私募融资" value="0"></el-option>
								<el-option label="投资咨询" value="1"></el-option>
								<el-option label="创业咨询" value="2"></el-option>
								<el-option label="战略规划" value="3"></el-option>
								<el-option label="合并收购" value="4"></el-option>
								<el-option label="IPO" value="5"></el-option>
								<el-option label="定向增发" value="6"></el-option>
								<el-option label="其他" value="7"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="CustomerDirection" label="客户发展方向">
							<el-select v-model="form.CustomerDirection" placeholder="请选择客户发展方向">
								<el-option label="政府" value="0"></el-option>
								<el-option label="高校" value="1"></el-option>
								<el-option label="海外" value="2"></el-option>
								<el-option label="研究院" value="3"></el-option>
								<el-option label="国企" value="4"></el-option>
								<el-option label="高新技术企业" value="5"></el-option>
								<el-option label="500强企业" value="6"></el-option>
								<el-option label="个人企业家" value="7"></el-option>
								<el-option label="其他" value="8"></el-option>
							</el-select>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为合伙人，则显示-->
				<div class="partner" v-show="partner">
					<h3>类别</h3>
					<div class="form-box basic width130">
						<el-form-item prop="NaturePartner" label="合伙人性质">
							<el-select v-model="form.NaturePartner" placeholder="请选择合伙人性质">
								<el-option label="募" value="0"></el-option>
								<el-option label="投" value="1"></el-option>
								<el-option label="管" value="2"></el-option>
								<el-option label="研" value="3"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="PartnershipMode" label="合伙人方式">
							<el-select v-model="form.PartnershipMode" placeholder="请选择合伙人方式">
								<el-option label="战略合伙人" value="0"></el-option>
								<el-option label="在职合伙人" value="1"></el-option>
							</el-select>
						</el-form-item>
					</div>
					<h3>资源圈</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="fieldExpertise" label="擅长领域">
							<el-select v-model="form.fieldExpertise" placeholder="请选择擅长领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="property" label="属性">
							<el-select v-model="form.property" placeholder="请选择属性">
								<el-option label="政府" value="0"></el-option>
								<el-option label="高校" value="1"></el-option>
								<el-option label="海外" value="2"></el-option>
								<el-option label="研究院" value="3"></el-option>
								<el-option label="国企" value="4"></el-option>
								<el-option label="高新技术企业" value="5"></el-option>
								<el-option label="500强企业" value="6"></el-option>
								<el-option label="个人企业家" value="7"></el-option>
								<el-option label="其他" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="territory" label="地域">
							<el-input v-model="form.territory" placeholder="请输入地域"></el-input>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为基金管理公司，则显示-->
				<div class="fundcompany" v-show="fundcompany">
					<h3>业务</h3>
					<div class="form-box basic width130">
						<el-form-item prop="MainGundType" label="主营基金类型">
							<el-select v-model="form.MainGundType" placeholder="请选择主营基金类型">
								<el-option label="科创类" value="0"></el-option>
								<el-option label="产业类" value="1"></el-option>
								<el-option label="股权类" value="2"></el-option>
								<el-option label="天使类" value="3"></el-option>
								<el-option label="VC类" value="4"></el-option>
								<el-option label="并购类" value="5"></el-option>
								<el-option label="固收类" value="6"></el-option>
								<el-option label="配置型" value="7"></el-option>
								<el-option label="其它" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="CFundPhase" label="基金阶段">
							<el-select v-model="form.CFundPhase" placeholder="请选择基金阶段">
								<el-option label="天使" value="0"></el-option>
								<el-option label="VC" value="1"></el-option>
								<el-option label="PE" value="2"></el-option>
								<el-option label="一级半" value="3"></el-option>
								<el-option label="二级" value="4"></el-option>
								<el-option label="其他" value="5"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="CfieldExpertise" label="覆盖领域">
							<el-select v-model="form.CfieldExpertise" placeholder="请选择覆盖领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="territory" label="在管基金">
							<el-input v-model="form.territory" placeholder="请输入在管基金"></el-input>
						</el-form-item>
						<el-form-item prop="CinvestmentStage" label="业务特色">
							<el-input v-model="form.CinvestmentStage" placeholder="请输入业务特色"></el-input>
						</el-form-item>
						<el-form-item prop="ConlinePlatform" label="有无线上对接平台">
							<el-radio-group v-model="form.ConlinePlatform">
								<el-radio label="0">是</el-radio>
								<el-radio label="1">否</el-radio>
								<el-radio label="2">筹备中</el-radio>
							</el-radio-group>
						</el-form-item>
					</div>
					<h3>成果资质</h3>
					<div class="form-box basic width130">
						<el-form-item prop="CtypicalCase" label="典型案例">
							<el-input v-model="form.CtypicalCase" placeholder="请输入典型案例"></el-input>
						</el-form-item>
						<el-form-item prop="CLicenceQualification" label="牌照资质">
							<el-input v-model="form.CLicenceQualification" placeholder="请输入牌照资质"></el-input>
						</el-form-item>
						<el-form-item prop="Cpartner" label="合作伙伴">
							<el-input v-model="form.Cpartner" placeholder="请输入合作伙伴"></el-input>
						</el-form-item>
					</div>
					<h3>诉求调研</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="CfundType" label="基金类型">
							<el-select v-model="form.CfundType" placeholder="请选择基金类型">
								<el-option label="科创类" value="0"></el-option>
								<el-option label="产业类" value="1"></el-option>
								<el-option label="股权类" value="2"></el-option>
								<el-option label="天使类" value="3"></el-option>
								<el-option label="VC类" value="4"></el-option>
								<el-option label="并购类" value="5"></el-option>
								<el-option label="固收类" value="6"></el-option>
								<el-option label="配置型" value="7"></el-option>
								<el-option label="其它" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="CfieldInvestment" label="投资领域">
							<el-select v-model="form.CfieldInvestment" placeholder="请选择投资领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="other" label="其它">
							<el-input v-model="form.other" placeholder="请输入其它"></el-input>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为投资机构，则显示-->
				<div class="investment" v-show="investment">
					<h3>业务</h3>
					<div class="form-box basic width130">
						<el-form-item prop="IfundType" label="投资方向">
							<el-select v-model="form.IfundType" placeholder="请选择投资方向">
								<el-option label="科创类" value="0"></el-option>
								<el-option label="产业类" value="1"></el-option>
								<el-option label="股权类" value="2"></el-option>
								<el-option label="天使类" value="3"></el-option>
								<el-option label="VC类" value="4"></el-option>
								<el-option label="并购类" value="5"></el-option>
								<el-option label="固收类" value="6"></el-option>
								<el-option label="配置型" value="7"></el-option>
								<el-option label="其它" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="IfieldInvestment" label="投资领域">
							<el-select v-model="form.IfieldInvestment" placeholder="请选择投资领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="IinvestmentStage" label="业务特色">
							<el-input v-model="form.IinvestmentStage" placeholder="请输入业务特色"></el-input>
						</el-form-item>
						<el-form-item prop="IonlinePlatform" label="有无线上对接平台">
							<el-radio-group v-model="form.IonlinePlatform">
								<el-radio label="0">是</el-radio>
								<el-radio label="1">否</el-radio>
								<el-radio label="2">筹备中</el-radio>
							</el-radio-group>
						</el-form-item>
					</div>
					<h3>成果资质</h3>
					<div class="form-box basic width130">
						<el-form-item prop="ILicenceQualification" label="牌照资质">
							<el-input v-model="form.ILicenceQualification" placeholder="请输入牌照资质"></el-input>
						</el-form-item>
						<el-form-item prop="TypicalExitCases" label="典型退出案例">
							<el-input v-model="form.TypicalExitCases" placeholder="请输入典型退出案例"></el-input>
						</el-form-item>
						<el-form-item prop="Ipartner" label="合作伙伴">
							<el-input v-model="form.Ipartner" placeholder="请输入合作伙伴"></el-input>
						</el-form-item>
					</div>
					<h3>投资诉求</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="ISfundType" label="投资方向">
							<el-select v-model="form.ISfundType" placeholder="请选择投资方向">
								<el-option label="科创类" value="0"></el-option>
								<el-option label="产业类" value="1"></el-option>
								<el-option label="股权类" value="2"></el-option>
								<el-option label="天使类" value="3"></el-option>
								<el-option label="VC类" value="4"></el-option>
								<el-option label="并购类" value="5"></el-option>
								<el-option label="固收类" value="6"></el-option>
								<el-option label="配置型" value="7"></el-option>
								<el-option label="其它" value="8"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="ISfieldExpertise" label="投资领域">
							<el-select v-model="form.ISfieldInvestment" placeholder="请选择投资领域">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="Iother" label="其它">
							<el-input v-model="form.Iother" placeholder="请输入其它"></el-input>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为政府，则显示-->
				<div class="government" v-show="government">
					<h3>政府资源</h3>
					<div class="form-box basic width130">
						<el-form-item prop="provideResources" label="提供资源">
							<el-input v-model="form.provideResources" placeholder="请输入提供资源"></el-input>
						</el-form-item>
						<el-form-item prop="ReferPolicy" label="参考政策">
							<el-input v-model="form.ReferPolicy" placeholder="请输入参考政策"></el-input>
						</el-form-item>
					</div>
					<h3>需求调研</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="introductionType" label="引进类型">
							<el-select v-model="form.introductionType" placeholder="请选择引进类型">
								<el-option label="人才" value="0"></el-option>
								<el-option label="资金" value="1"></el-option>
								<el-option label="企业" value="2"></el-option>
								<el-option label="项目" value="3"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="IntroductionTarget" label="引进目标">
							<el-input v-model="form.IntroductionTarget" placeholder="请输入引进目标"></el-input>
						</el-form-item>
						<el-form-item prop="DemandConditions" label="要求条件">
							<el-input v-model="form.DemandConditions" placeholder="请输入要求条件"></el-input>
						</el-form-item>
					</div>
				</div>

				<!--如果角色选择为游客，则显示-->
				<div class="visitor" v-show="visitor">
					<h3>浏览喜好</h3>
					<div class="form-box basic width130">
						<el-form-item prop="vocation" label="行业">
							<el-select v-model="form.vocation" placeholder="请选择行业">
								<el-option label="人工智能与机器人" value="0"></el-option>
								<el-option label="信息电子与大数据" value="1"></el-option>
								<el-option label="智能制造与工业4.0" value="2"></el-option>
								<el-option label="环境保护与新能源" value="3"></el-option>
								<el-option label="生物医疗与大健康" value="4"></el-option>
								<el-option label="绿色建筑与房地产" value="5"></el-option>
								<el-option label="金融科技与新资管" value="6"></el-option>
								<el-option label="消费升级与大文旅" value="7"></el-option>
								<el-option label="工艺美术与新媒体" value="8"></el-option>
								<el-option label="其它" value="9"></el-option>
							</el-select>
						</el-form-item>
						<el-form-item prop="direction" label="方向">
							<el-select v-model="form.direction" placeholder="请选择方向">
								<el-option label="创业" value="0"></el-option>
								<el-option label="募资" value="1"></el-option>
								<el-option label="投资" value="2"></el-option>
								<el-option label="研究" value="3"></el-option>
								<el-option label="管理" value="4"></el-option>
								<el-option label="FA" value="5"></el-option>
							</el-select>
						</el-form-item>
					</div>
					<h3>浏览目标</h3>
					<div class="form-box basic width130 border-bottom">
						<el-form-item prop="appeal" label="诉求">
							<el-select v-model="form.appeal" placeholder="请选择诉求">
								<el-option label="找资金" value="0"></el-option>
								<el-option label="找项目" value="1"></el-option>
								<el-option label="找人脉" value="2"></el-option>
								<el-option label="找地区" value="3"></el-option>
								<el-option label="找平台" value="4"></el-option>
								<el-option label="找服务" value="5"></el-option>
								<el-option label="找培训" value="6"></el-option>
								<el-option label="其他" value="7"></el-option>
							</el-select>
						</el-form-item>
					</div>
				</div>

				<!--增值服务-->
				<div class="inforTitle">
					<h2>增值服务</h2>
				</div>
				<h3>免费报告</h3>
				<div class="form-box basic width110 border-bottom">
					<el-form-item label="类型" prop="FreeReport">
						<el-select v-model="form.FreeReport" placeholder="请选择类型">
							<el-option label="天使" value="0"></el-option>
							<el-option label="VC" value="1"></el-option>
							<el-option label="PE" value="2"></el-option>
							<el-option label="并购" value="3"></el-option>
							<el-option label="上市" value="4"></el-option>
							<el-option label="资产管理" value="5"></el-option>
							<el-option label="其它" value="6"></el-option>
						</el-select>
					</el-form-item>
					<el-form-item label="语言" prop="language">
						<el-select v-model="form.language" placeholder="请选择语言">
							<el-option label="中文" value="chinese"></el-option>
							<el-option label="英文" value="english"></el-option>
						</el-select>
					</el-form-item>
					<el-form-item label="同步接收邮箱 " prop="receiveEmail">
						<el-input v-model="form.receiveEmail" placeholder="不限个数,多个邮箱地址用逗号隔开"></el-input>
					</el-form-item>
				</div>
				<!--增值服务-->
				<div class="inforTitle">
					<h2>附件</h2>
				</div>
				<h3>项目成果性展示</h3>
				<div class="form-box basic width110 border-bottom">
					<el-form-item label="附件上传 ">
						<el-input placeholder="不限个数,多个邮箱地址用逗号隔开"></el-input>
					</el-form-item>
				</div>
				<el-button type="primary" @click="onSubmit('form')">提交</el-button>
			</el-form>
		</div>

		<towbottom></towbottom>
	</div>
</template>

<script scope>
	import towtop from '@/components/testTop'
	import towbottom from '@/components/testBottom'
	export default {
		data() {
			return {
				RoleId: this.$route.query.roleId,
				Phone: this.$route.query.phone,
				userType: '',
				form: {},
				ESTP: false, //创业者 1
				investor: false, //投资人 2
				FAInstitution: false, //FA机构 3
				partner: false, //合伙人 4
				fundcompany: false, //基金管理公司 5
				investment: false, //投资机构 6
				government: false, //政府 7
				visitor: false, //游客 8
				rules: {
					name: [{
							required: true,
							message: '请输入姓名',
							trigger: 'blur'
						},
						{
							min: 3,
							max: 5,
							message: '姓名长度在 3 到 5 个字符',
							trigger: 'blur'
						}
					],
					cellphone: [{
							required: true,
							message: '请输入手机号',
							trigger: 'blur'
						},
						{
							type: 'number',
							message: '手机号格式不正确',
						}
					],
					gender: [{
						required: true,
						message: '请输入性别',
						trigger: 'blur'
					}],
					Wechat: [{
						required: true,
						message: '请输入微信号',
						trigger: 'blur'
					}],
					nationality: [{
						required: true,
						message: '请输入国籍',
						trigger: 'blur'
					}],
					email: [{
							required: true,
							message: '请输入邮箱',
							trigger: 'blur'
						},
						{
							type: 'email',
							required: true,
							message: '邮箱格式不正确',
							trigger: 'blur'
						}
					],
					idType: [{
						required: true,
						message: '请选择证件类型',
						trigger: 'change'
					}],
					idTypeNumber: [{
						required: true,
						message: '请输入证件号',
						trigger: 'blur'
					}],
					education: [{
						required: true,
						message: '请选择最高学历',
						trigger: 'change'
					}],
					school: [{
						required: true,
						message: '请输入学校',
						trigger: 'blur'
					}],
					professional: [{
						required: true,
						message: '请输入专业',
						trigger: 'blur'
					}],
					graduationDate: [{
						required: true,
						message: '请选择毕业日期',
						trigger: 'blur'
					}],
					work: [{
						required: true,
						message: '请输入单位名称',
						trigger: 'blur'
					}],
					duty: [{
						required: true,
						message: '请输入职务',
						trigger: 'blur'
					}],
					rank: [{
						required: true,
						message: '请选择职级',
						trigger: 'change'
					}],
					city: [{
						required: true,
						message: '请输入所在地区',
						trigger: 'blur'
					}],
					firstBusiness: [{
						required: true,
						message: '请选择是否为首次创业',
						trigger: 'change'
					}],
					entrepreneurship: [{
						required: true,
						message: '请选择创业领域',
						trigger: 'change'
					}],
					AnnualRevenue: [{
						required: true,
						message: '请输入每年营收',
						trigger: 'blur'
					}],
					financingScale: [{
						required: true,
						message: '请输入融资规模',
						trigger: 'blur'
					}],
					customerSize: [{
						required: true,
						message: '请输入客户规模',
						trigger: 'blur'
					}],
					scale: [{
						required: true,
						message: '请输入企业规模',
						trigger: 'blur'
					}],
					targetElse: [{
						required: true,
						message: '请输入其他',
						trigger: 'blur'
					}],
					summarize: [{
						required: true,
						message: '请输入创业项目概述',
						trigger: 'blur'
					}],
					CGAnnualRevenue: [{
						required: true,
						message: '请输入每年营收',
						trigger: 'blur'
					}],
					CGfinancingScale: [{
						required: true,
						message: '请输入融资规模',
						trigger: 'blur'
					}],
					CGcustomerSize: [{
						required: true,
						message: '请输入客户规模',
						trigger: 'blur'
					}],
					resourceNeeds: [{
						required: true,
						message: '请选择资源需求',
						trigger: 'change'
					}]
				}
			}

		},
		components: {
			towtop,
			towbottom
		},
		created() {
			this.getUserType();
		},
		methods: {
			getUserType() {
				var that = this;
				console.log(that.RoleId)
				if(that.RoleId == 1) {
					that.UserType = "创业者";
					that.ESTP = true; //创业者 1
					that.investor = false; //投资人 2
					that.FAInstitution = false; //FA机构 3
					that.partner = false; //合伙人 4
					that.fundcompany = false; //基金管理公司 5
					that.investment = false; //投资机构 6
					that.government = false; //政府 7
					that.visitor = false //游客 8
				} else if(that.RoleId == 2) {
					that.UserType = "投资人";
				} else if(that.RoleId == 3) {
					that.UserType = "FA机构";
				} else if(that.RoleId == 4) {
					that.UserType = "合伙人";
				} else if(that.RoleId == 5) {
					that.UserType = "基金管理公司";
				} else if(that.RoleId == 6) {
					that.UserType = "投资机构";
				} else if(that.RoleId == 7) {
					that.UserType = "政府";
				} else {
					that.UserType = "游客";
				}
			},
			onSubmit(formName) {
				var that = this;
				console.log(that.form.achievement)
				if(that.form.firstBusiness == 0 && that.form.achievement==undefined) {
					 callback(new Error('请输入创业经历与成果'));
				} else {

				}
				//角色为创业者
				if(that.RoleId == 1) {
					var data = {
						'name': that.form.name, //姓名
						'cellphone': that.form.cellphone, //手机号
						'gender': that.form.gender, //性别
						'Wechat': that.form.Wechat, //微信号
						'nationality': that.form.nationality, //国籍
						'email': that.form.email, //邮箱
						'nation': that.form.nation, //民族
						'idType': that.form.idType, //证件类型
						'maritalStatus': that.form.maritalStatus, //婚姻状况
						'idTypeNumber': that.form.idTypeNumber, //证件号码
						'education': that.form.education, //最高学历
						'school': that.form.school, //学校
						'professional': that.form.professional, //专业
						'graduationDate': that.form.graduationDate, //毕业日期
						'work': that.form.work, //单位
						'duty': that.form.duty, //职务
						'rank': that.form.rank, //职级
						'city': that.form.city, //所在地区 
						'workbackground': that.form.workbackground, //工作经历
						'firstBusiness': that.form.firstBusiness, //是否为首次创业
						'achievement': that.form.achievement, //创业经历与成果
						'businessbackground': that.form.businessbackground, //工作经历
						'entrepreneurship': that.form.entrepreneurship, //创业领域
						'AnnualRevenue': that.form.AnnualRevenue, //每年营收
						'financingScale': that.form.financingScale, //融资规模
						'customerSize': that.form.customerSize, //客户规模
						'scale': that.form.scale, //企业规模
						'targetElse': that.form.targetElse, //其它
						'summarize': that.form.summarize, //创业项目概述
						'CGAnnualRevenue': that.form.CGAnnualRevenue, //每年营收
						'CGfinancingScale': that.form.CGfinancingScale, //融资规模
						'CGcustomerSize': that.form.CGcustomerSize, //客户规模
						'resourceNeeds': that.form.resourceNeeds, //资源需求
						'FreeReport': that.form.FreeReport, //免费报告类型
						'language': that.form.language, //免费报告语言
						'receiveEmail': that.form.receiveEmail //同步接收邮箱
					};

					that.$refs[formName].validate((valid) => {
						if(valid) {

							alert('submit!');
						} else {
							console.log('error submit!!');
							return false;
						}
					});
				} else {

				}

			}
		}
	}
</script>
<!--Element-ui重置样式-->
<style>
	.el-input--small .el-input__inner {
		height: 44px;
		line-height: 44px;
	}
	
	.el-form-item--small .el-form-item__content,
	.el-form-item--small .el-form-item__label {
		line-height: 44px;
	}
	
	.width80 .el-form-item__label {
		width: 80px;
	}
	
	.width110 .el-form-item__label {
		width: 110px;
	}
	
	.width130 .el-form-item__label {
		width: 130px;
	}
	
	.form-box .el-input__inner {
		width: 240px;
	}
	
	.basic .el-form-item {
		margin-right: 50px;
	}
	
	.hiEducation .el-radio__label {
		font-size: 16px;
	}
	
	.hiEducation .el-form-item__label {
		font-size: 16px;
	}
	
	.basic .el-textarea__inner {
		width: 674px;
		height: 150px;
	}
	
	.form-box .reset-input .el-input__inner {
		width: 140px;
	}
	
	.reset-input .el-input {
		width: 140px;
	}
	
	.reset-input .el-form-item__content {
		width: 700px;
	}
	
	.authentication .el-button--small {
		padding: 14px 117px;
		margin: 10px auto 60px;
		display: block;
		font-size: 16px;
	}
	
	.authentication .el-button--primary {
		background-color: #0546B4;
		border-color: #0546B4;
	}
	
	.multiInput {
		margin-right: 10px !important;
	}
	
	.multiInput .el-form-item__label {
		width: 110px !important;
		font-size: 14px;
		font-weight: normal;
	}
</style>
<!--页面样式-->
<style scoped>
	.border-bottom {
		border-bottom: none !important;
	}
	
	.container {
		width: 1000px;
	}
	
	.headerBg {
		background: #fff;
		box-shadow: 0 3px 11px 0 rgba(51, 51, 51, 0.50);
	}
	
	.back {
		float: right;
		line-height: 55px;
		color: #0546B4;
		font-size: 18px;
	}
	
	.information {
		margin-top: 135px;
		margin-bottom: 44px;
	}
	
	.user {
		display: flex;
		margin-bottom: 30px;
	}
	
	.user img {
		width: 70px;
		height: 70px;
		margin-right: 20px;
	}
	
	.user p {
		line-height: 70px;
		font-size: 20px;
	}
	
	.information h2 {
		font-size: 26px;
		display: inline-block;
	}
	
	.information span {
		font-size: 16px;
		margin-left: 20px;
	}
	
	.inforTitle {
		width: 1000px;
		border-bottom: 1px solid #D8D8D8;
		height: 38px;
	}
	
	.inforTitle h2 {
		font-size: 20px;
		line-height: 38px;
		font-weight: 700;
	}
	
	.authentication .container .basic {
		padding: 0 0 10px 110px;
	}
	
	.authentication .container .form-box {
		width: 1000px;
		box-sizing: border-box;
		border-bottom: 1px dashed #ccc;
	}
	
	.authentication .container h3 {
		font-size: 16px;
		color: #333;
		margin: 40px 0 20px 70px;
	}
	
	label {
		font-weight: normal;
	}
	
	h3 {
		font-weight: 700;
	}
	
	.basic form {
		margin-left: 130px;
	}
	
	.target {
		display: inline-block;
		position: relative;
		margin-right: 16px;
		margin-bottom: 10px;
	}
	
	.target span {
		position: absolute;
		right: 10px;
	}
	
	.reset-input .target:nth-child(5) {
		padding-left: 29px;
	}
	
	.authentication .container .basic p {
		display: inline-block;
		height: 44px;
		line-height: 44px;
		width: 118px;
		text-align: right;
		font-weight: 700;
		color: #606266
	}
</style>