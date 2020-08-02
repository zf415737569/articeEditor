<template>
	<div>
		<div class="edit_notice_wrap hidden">
			<p class="edit_notice_title">
				想改哪里 <span class="edit_notice_y">点</span>哪里
			</p>
			<img
				class="edit_notice_img"
				src="https://staticoss.bxdaka.com/static/images/edit_notice.png"
				alt=""
			/>
			<div class="notice_btn">
				<div class="notice_btn_item no_notice">不再提示</div>
				<div class="notice_btn_item notice_known">我知道了</div>
			</div>
		</div>
		<div class="container">
			<!--编辑按钮-->
			<div class="art_section_edit_wrap" style="display: none;">
				<div class="art_section_edit" style="width: 345px;">
					<div class="edit_btn_item" @click="deleteEl">
						<!-- <div class="edit_btn_delete_icon"></div> -->
						<span class="edit_btn_txt">删除</span>
					</div>
					<div class="edit_btn_item edit_edit_btn" @click="editEdit">
						<!-- <div class="edit_btn_edit_icon"></div> -->
						<span class="edit_btn_txt">修改</span>
					</div>
					<div class="edit_btn_item add_text_btn" @click="editAddText">
						<!-- <div class="edit_btn_txt_icon"></div> -->
						<span class="edit_btn_txt">文字</span>
					</div>

					<van-uploader
						class="edit_btn_item add_img_btn"
						:max-count="1"
						:after-read="afterRead3"
					>
						<div @click="editAddImg">
							<!-- <div class="edit_btn_img_icon"></div> -->
							<span class="edit_btn_txt">图片</span>
						</div>
					</van-uploader>

					<!-- <div class="edit_btn_item add_pro_btn" onclick="editAddPro()">
			<div class="edit_btn_pro_icon"></div>
			<span class="edit_btn_txt">产品</span>
		  </div> -->
				</div>
			</div>
			<!--修改， 添加文本弹框-->
			<div id="edit_text" class="weui-popup__container">
				<div class="weui-popup__overlay"></div>
				<div class="weui-popup__modal needsclick">
					<div class="edit_text_con">
						<div id="summernote" style="display: none;"></div>
						<div class="note-editor note-frame panel panel-default">
							<div class="note-dropzone">
								<div class="note-dropzone-message"></div>
							</div>
							<div class="note-toolbar panel-heading" role="toolbar">
								<div class="note-btn-group btn-group note-style">
									<div class="note-btn-group btn-group">
										<button
											type="button"
											class="note-btn btn btn-default btn-sm dropdown-toggle"
											role="button"
											tabindex="-1"
											data-toggle="dropdown"
											title=""
											aria-label="Style"
											data-original-title="Style"
										>
											<i class="note-icon-magic"></i>
											<span class="note-icon-caret"></span>
										</button>
										<ul
											class="dropdown-menu dropdown-style"
											role="list"
											aria-label="Style"
										>
											<li role="listitem" aria-label="p">
												<a href="#" data-value="p"
													><p>Normal</p></a
												>
											</li>
											<li role="listitem" aria-label="blockquote">
												<a href="#" data-value="blockquote"
													><blockquote>Quote</blockquote></a
												>
											</li>
											<li role="listitem" aria-label="pre">
												<a href="#" data-value="pre">
													<pre>Code</pre>
												</a>
											</li>
											<li role="listitem" aria-label="h1">
												<a href="#" data-value="h1"
													><h1>Header 1</h1></a
												>
											</li>
											<li role="listitem" aria-label="h2">
												<a href="#" data-value="h2"
													><h2>Header 2</h2></a
												>
											</li>
											<li role="listitem" aria-label="h3">
												<a href="#" data-value="h3"
													><h3>Header 3</h3></a
												>
											</li>
											<li role="listitem" aria-label="h4">
												<a href="#" data-value="h4"
													><h4>Header 4</h4></a
												>
											</li>
											<li role="listitem" aria-label="h5">
												<a href="#" data-value="h5"
													><h5>Header 5</h5></a
												>
											</li>
											<li role="listitem" aria-label="h6">
												<a href="#" data-value="h6"
													><h6>Header 6</h6></a
												>
											</li>
										</ul>
									</div>
								</div>
								<div class="note-btn-group btn-group note-font">
									<button
										type="button"
										class="note-btn btn btn-default btn-sm note-btn-bold"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Bold (CTRL+B)"
										data-original-title="Bold (CTRL+B)"
									>
										<i class="note-icon-bold"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm note-btn-underline"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Underline (CTRL+U)"
										data-original-title="Underline (CTRL+U)"
									>
										<i class="note-icon-underline"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Remove Font Style (CTRL+\)"
										data-original-title="Remove Font Style (CTRL+\)"
									>
										<i class="note-icon-eraser"></i>
									</button>
								</div>
								<div class="note-btn-group btn-group note-fontname">
									<div class="note-btn-group btn-group">
										<button
											type="button"
											class="note-btn btn btn-default btn-sm dropdown-toggle"
											role="button"
											tabindex="-1"
											data-toggle="dropdown"
											title=""
											aria-label="Font Family"
											data-original-title="Font Family"
										>
											<span
												class="note-current-fontname"
												style="font-family: 微软雅黑;"
												>微软雅黑</span
											>
											<span class="note-icon-caret"></span>
										</button>
										<ul
											class="dropdown-menu note-check dropdown-fontname"
											role="list"
											aria-label="Font Family"
										>
											<li role="listitem" aria-label="Arial">
												<a href="#" data-value="Arial"
													><i class="note-icon-menu-check"></i>
													<span style="font-family: 'Arial';"
														>Arial</span
													></a
												>
											</li>
											<li role="listitem" aria-label="Arial Black">
												<a href="#" data-value="Arial Black"
													><i class="note-icon-menu-check"></i>
													<span
														style="
															font-family: 'Arial Black';
														"
														>Arial Black</span
													></a
												>
											</li>
											<li
												role="listitem"
												aria-label="Comic Sans MS"
											>
												<a href="#" data-value="Comic Sans MS"
													><i class="note-icon-menu-check"></i>
													<span
														style="
															font-family: 'Comic Sans MS';
														"
														>Comic Sans MS</span
													></a
												>
											</li>
											<li role="listitem" aria-label="Courier New">
												<a href="#" data-value="Courier New"
													><i class="note-icon-menu-check"></i>
													<span
														style="
															font-family: 'Courier New';
														"
														>Courier New</span
													></a
												>
											</li>
											<li role="listitem" aria-label="Helvetica">
												<a href="#" data-value="Helvetica"
													><i class="note-icon-menu-check"></i>
													<span
														style="font-family: 'Helvetica';"
														>Helvetica</span
													></a
												>
											</li>
											<li role="listitem" aria-label="Impact">
												<a href="#" data-value="Impact"
													><i class="note-icon-menu-check"></i>
													<span style="font-family: 'Impact';"
														>Impact</span
													></a
												>
											</li>
											<li role="listitem" aria-label="Tahoma">
												<a href="#" data-value="Tahoma"
													><i class="note-icon-menu-check"></i>
													<span style="font-family: 'Tahoma';"
														>Tahoma</span
													></a
												>
											</li>
											<li
												role="listitem"
												aria-label="Times New Roman"
											>
												<a href="#" data-value="Times New Roman"
													><i class="note-icon-menu-check"></i>
													<span
														style="
															font-family: 'Times New Roman';
														"
														>Times New Roman</span
													></a
												>
											</li>
											<li role="listitem" aria-label="Verdana">
												<a href="#" data-value="Verdana"
													><i class="note-icon-menu-check"></i>
													<span style="font-family: 'Verdana';"
														>Verdana</span
													></a
												>
											</li>
											<li role="listitem" aria-label="微软雅黑">
												<a
													href="#"
													data-value="微软雅黑"
													class="checked"
													><i class="note-icon-menu-check"></i>
													<span style="font-family: '微软雅黑';"
														>微软雅黑</span
													></a
												>
											</li>
											<li
												role="listitem"
												aria-label="Microsoft Yahei"
											>
												<a href="#" data-value="Microsoft Yahei"
													><i class="note-icon-menu-check"></i>
													<span
														style="
															font-family: 'Microsoft Yahei';
														"
														>Microsoft Yahei</span
													></a
												>
											</li>
										</ul>
									</div>
								</div>
								<div class="note-btn-group btn-group note-color">
									<div
										class="note-btn-group btn-group note-color note-color-all"
									>
										<button
											type="button"
											class="note-btn btn btn-default btn-sm note-current-color-button"
											role="button"
											tabindex="-1"
											title=""
											aria-label="Recent Color"
											data-original-title="Recent Color"
											data-backcolor="#FFFF00"
										>
											<i
												class="note-icon-font note-recent-color"
												style="
													background-color: rgb(255, 255, 0);
												"
											></i></button
										><button
											type="button"
											class="note-btn btn btn-default btn-sm dropdown-toggle"
											role="button"
											tabindex="-1"
											data-toggle="dropdown"
											title=""
											aria-label="More Color"
											data-original-title="More Color"
										>
											<span class="note-icon-caret"></span>
										</button>
										<ul class="dropdown-menu" role="list">
											<div class="note-palette">
												<div class="note-palette-title">
													Background Color
												</div>
												<div>
													<button
														type="button"
														class="note-color-reset btn btn-light"
														data-event="backColor"
														data-value="inherit"
													>
														Transparent
													</button>
												</div>
												<div
													class="note-holder"
													data-event="backColor"
												>
													<div class="note-color-palette">
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #000000;
																"
																data-event="backColor"
																data-value="#000000"
																title=""
																aria-label="Black"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Black"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #424242;
																"
																data-event="backColor"
																data-value="#424242"
																title=""
																aria-label="Tundora"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tundora"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #636363;
																"
																data-event="backColor"
																data-value="#636363"
																title=""
																aria-label="Dove Gray"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Dove Gray"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9c9c94;
																"
																data-event="backColor"
																data-value="#9C9C94"
																title=""
																aria-label="Star Dust"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Star Dust"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #cec6ce;
																"
																data-event="backColor"
																data-value="#CEC6CE"
																title=""
																aria-label="Pale Slate"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Pale Slate"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #efefef;
																"
																data-event="backColor"
																data-value="#EFEFEF"
																title=""
																aria-label="Gallery"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Gallery"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #f7f7f7;
																"
																data-event="backColor"
																data-value="#F7F7F7"
																title=""
																aria-label="Alabaster"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Alabaster"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="White"
																data-toggle="button"
																tabindex="-1"
																data-original-title="White"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ff0000;
																"
																data-event="backColor"
																data-value="#FF0000"
																title=""
																aria-label="Red"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Red"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ff9c00;
																"
																data-event="backColor"
																data-value="#FF9C00"
																title=""
																aria-label="Orange Peel"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Orange Peel"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffff00;
																"
																data-event="backColor"
																data-value="#FFFF00"
																title=""
																aria-label="Yellow"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Yellow"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #00ff00;
																"
																data-event="backColor"
																data-value="#00FF00"
																title=""
																aria-label="Green"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Green"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #00ffff;
																"
																data-event="backColor"
																data-value="#00FFFF"
																title=""
																aria-label="Cyan"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cyan"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #0000ff;
																"
																data-event="backColor"
																data-value="#0000FF"
																title=""
																aria-label="Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9c00ff;
																"
																data-event="backColor"
																data-value="#9C00FF"
																title=""
																aria-label="Electric Violet"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Electric Violet"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ff00ff;
																"
																data-event="backColor"
																data-value="#FF00FF"
																title=""
																aria-label="Magenta"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Magenta"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #f7c6ce;
																"
																data-event="backColor"
																data-value="#F7C6CE"
																title=""
																aria-label="Azalea"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Azalea"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffe7ce;
																"
																data-event="backColor"
																data-value="#FFE7CE"
																title=""
																aria-label="Karry"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Karry"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffefc6;
																"
																data-event="backColor"
																data-value="#FFEFC6"
																title=""
																aria-label="Egg White"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Egg White"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #d6efd6;
																"
																data-event="backColor"
																data-value="#D6EFD6"
																title=""
																aria-label="Zanah"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Zanah"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #cedee7;
																"
																data-event="backColor"
																data-value="#CEDEE7"
																title=""
																aria-label="Botticelli"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Botticelli"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #cee7f7;
																"
																data-event="backColor"
																data-value="#CEE7F7"
																title=""
																aria-label="Tropical Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tropical Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #d6d6e7;
																"
																data-event="backColor"
																data-value="#D6D6E7"
																title=""
																aria-label="Mischka"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Mischka"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e7d6de;
																"
																data-event="backColor"
																data-value="#E7D6DE"
																title=""
																aria-label="Twilight"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Twilight"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e79c9c;
																"
																data-event="backColor"
																data-value="#E79C9C"
																title=""
																aria-label="Tonys Pink"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tonys Pink"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffc69c;
																"
																data-event="backColor"
																data-value="#FFC69C"
																title=""
																aria-label="Peach Orange"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Peach Orange"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffe79c;
																"
																data-event="backColor"
																data-value="#FFE79C"
																title=""
																aria-label="Cream Brulee"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cream Brulee"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #b5d6a5;
																"
																data-event="backColor"
																data-value="#B5D6A5"
																title=""
																aria-label="Sprout"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Sprout"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #a5c6ce;
																"
																data-event="backColor"
																data-value="#A5C6CE"
																title=""
																aria-label="Casper"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Casper"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9cc6ef;
																"
																data-event="backColor"
																data-value="#9CC6EF"
																title=""
																aria-label="Perano"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Perano"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #b5a5d6;
																"
																data-event="backColor"
																data-value="#B5A5D6"
																title=""
																aria-label="Cold Purple"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cold Purple"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #d6a5bd;
																"
																data-event="backColor"
																data-value="#D6A5BD"
																title=""
																aria-label="Careys Pink"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Careys Pink"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e76363;
																"
																data-event="backColor"
																data-value="#E76363"
																title=""
																aria-label="Mandy"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Mandy"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #f7ad6b;
																"
																data-event="backColor"
																data-value="#F7AD6B"
																title=""
																aria-label="Rajah"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Rajah"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffd663;
																"
																data-event="backColor"
																data-value="#FFD663"
																title=""
																aria-label="Dandelion"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Dandelion"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #94bd7b;
																"
																data-event="backColor"
																data-value="#94BD7B"
																title=""
																aria-label="Olivine"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Olivine"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #73a5ad;
																"
																data-event="backColor"
																data-value="#73A5AD"
																title=""
																aria-label="Gulf Stream"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Gulf Stream"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #6badde;
																"
																data-event="backColor"
																data-value="#6BADDE"
																title=""
																aria-label="Viking"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Viking"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #8c7bc6;
																"
																data-event="backColor"
																data-value="#8C7BC6"
																title=""
																aria-label="Blue Marguerite"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Blue Marguerite"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #c67ba5;
																"
																data-event="backColor"
																data-value="#C67BA5"
																title=""
																aria-label="Puce"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Puce"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ce0000;
																"
																data-event="backColor"
																data-value="#CE0000"
																title=""
																aria-label="Guardsman Red"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Guardsman Red"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e79439;
																"
																data-event="backColor"
																data-value="#E79439"
																title=""
																aria-label="Fire Bush"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Fire Bush"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #efc631;
																"
																data-event="backColor"
																data-value="#EFC631"
																title=""
																aria-label="Golden Dream"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Golden Dream"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #6ba54a;
																"
																data-event="backColor"
																data-value="#6BA54A"
																title=""
																aria-label="Chelsea Cucumber"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Chelsea Cucumber"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #4a7b8c;
																"
																data-event="backColor"
																data-value="#4A7B8C"
																title=""
																aria-label="Smalt Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Smalt Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #3984c6;
																"
																data-event="backColor"
																data-value="#3984C6"
																title=""
																aria-label="Boston Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Boston Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #634aa5;
																"
																data-event="backColor"
																data-value="#634AA5"
																title=""
																aria-label="Butterfly Bush"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Butterfly Bush"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #a54a7b;
																"
																data-event="backColor"
																data-value="#A54A7B"
																title=""
																aria-label="Cadillac"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cadillac"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9c0000;
																"
																data-event="backColor"
																data-value="#9C0000"
																title=""
																aria-label="Sangria"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Sangria"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #b56308;
																"
																data-event="backColor"
																data-value="#B56308"
																title=""
																aria-label="Mai Tai"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Mai Tai"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #bd9400;
																"
																data-event="backColor"
																data-value="#BD9400"
																title=""
																aria-label="Buddha Gold"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Buddha Gold"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #397b21;
																"
																data-event="backColor"
																data-value="#397B21"
																title=""
																aria-label="Forest Green"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Forest Green"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #104a5a;
																"
																data-event="backColor"
																data-value="#104A5A"
																title=""
																aria-label="Eden"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Eden"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #085294;
																"
																data-event="backColor"
																data-value="#085294"
																title=""
																aria-label="Venice Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Venice Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #311873;
																"
																data-event="backColor"
																data-value="#311873"
																title=""
																aria-label="Meteorite"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Meteorite"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #731842;
																"
																data-event="backColor"
																data-value="#731842"
																title=""
																aria-label="Claret"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Claret"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #630000;
																"
																data-event="backColor"
																data-value="#630000"
																title=""
																aria-label="Rosewood"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Rosewood"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #7b3900;
																"
																data-event="backColor"
																data-value="#7B3900"
																title=""
																aria-label="Cinnamon"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cinnamon"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #846300;
																"
																data-event="backColor"
																data-value="#846300"
																title=""
																aria-label="Olive"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Olive"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #295218;
																"
																data-event="backColor"
																data-value="#295218"
																title=""
																aria-label="Parsley"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Parsley"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #083139;
																"
																data-event="backColor"
																data-value="#083139"
																title=""
																aria-label="Tiber"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tiber"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #003163;
																"
																data-event="backColor"
																data-value="#003163"
																title=""
																aria-label="Midnight Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Midnight Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #21104a;
																"
																data-event="backColor"
																data-value="#21104A"
																title=""
																aria-label="Valentino"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Valentino"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #4a1031;
																"
																data-event="backColor"
																data-value="#4A1031"
																title=""
																aria-label="Loulou"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Loulou"
															></button>
														</div>
													</div>
												</div>
												<div>
													<button
														type="button"
														class="note-color-select btn"
														data-event="openPalette"
														data-value="backColorPicker"
													>
														Select
													</button>
													<input
														type="color"
														id="backColorPicker"
														class="note-btn note-color-select-btn"
														value="#FFFF00"
														data-event="backColorPalette"
													/>
												</div>
												<div
													class="note-holder-custom"
													id="backColorPalette"
													data-event="backColor"
												>
													<div class="note-color-palette">
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="backColor"
																data-value="#FFFFFF"
																title=""
																aria-label="#FFFFFF"
																data-toggle="button"
																tabindex="-1"
																data-original-title="#FFFFFF"
															></button>
														</div>
													</div>
												</div>
											</div>
											<div class="note-palette">
												<div class="note-palette-title">
													Foreground Color
												</div>
												<div>
													<button
														type="button"
														class="note-color-reset btn btn-light"
														data-event="removeFormat"
														data-value="foreColor"
													>
														Reset to default
													</button>
												</div>
												<div
													class="note-holder"
													data-event="foreColor"
												>
													<div class="note-color-palette">
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #000000;
																"
																data-event="foreColor"
																data-value="#000000"
																title=""
																aria-label="Black"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Black"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #424242;
																"
																data-event="foreColor"
																data-value="#424242"
																title=""
																aria-label="Tundora"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tundora"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #636363;
																"
																data-event="foreColor"
																data-value="#636363"
																title=""
																aria-label="Dove Gray"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Dove Gray"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9c9c94;
																"
																data-event="foreColor"
																data-value="#9C9C94"
																title=""
																aria-label="Star Dust"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Star Dust"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #cec6ce;
																"
																data-event="foreColor"
																data-value="#CEC6CE"
																title=""
																aria-label="Pale Slate"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Pale Slate"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #efefef;
																"
																data-event="foreColor"
																data-value="#EFEFEF"
																title=""
																aria-label="Gallery"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Gallery"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #f7f7f7;
																"
																data-event="foreColor"
																data-value="#F7F7F7"
																title=""
																aria-label="Alabaster"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Alabaster"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffffff;
																"
																data-event="foreColor"
																data-value="#FFFFFF"
																title=""
																aria-label="White"
																data-toggle="button"
																tabindex="-1"
																data-original-title="White"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ff0000;
																"
																data-event="foreColor"
																data-value="#FF0000"
																title=""
																aria-label="Red"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Red"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ff9c00;
																"
																data-event="foreColor"
																data-value="#FF9C00"
																title=""
																aria-label="Orange Peel"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Orange Peel"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffff00;
																"
																data-event="foreColor"
																data-value="#FFFF00"
																title=""
																aria-label="Yellow"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Yellow"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #00ff00;
																"
																data-event="foreColor"
																data-value="#00FF00"
																title=""
																aria-label="Green"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Green"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #00ffff;
																"
																data-event="foreColor"
																data-value="#00FFFF"
																title=""
																aria-label="Cyan"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cyan"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #0000ff;
																"
																data-event="foreColor"
																data-value="#0000FF"
																title=""
																aria-label="Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9c00ff;
																"
																data-event="foreColor"
																data-value="#9C00FF"
																title=""
																aria-label="Electric Violet"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Electric Violet"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ff00ff;
																"
																data-event="foreColor"
																data-value="#FF00FF"
																title=""
																aria-label="Magenta"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Magenta"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #f7c6ce;
																"
																data-event="foreColor"
																data-value="#F7C6CE"
																title=""
																aria-label="Azalea"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Azalea"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffe7ce;
																"
																data-event="foreColor"
																data-value="#FFE7CE"
																title=""
																aria-label="Karry"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Karry"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffefc6;
																"
																data-event="foreColor"
																data-value="#FFEFC6"
																title=""
																aria-label="Egg White"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Egg White"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #d6efd6;
																"
																data-event="foreColor"
																data-value="#D6EFD6"
																title=""
																aria-label="Zanah"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Zanah"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #cedee7;
																"
																data-event="foreColor"
																data-value="#CEDEE7"
																title=""
																aria-label="Botticelli"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Botticelli"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #cee7f7;
																"
																data-event="foreColor"
																data-value="#CEE7F7"
																title=""
																aria-label="Tropical Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tropical Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #d6d6e7;
																"
																data-event="foreColor"
																data-value="#D6D6E7"
																title=""
																aria-label="Mischka"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Mischka"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e7d6de;
																"
																data-event="foreColor"
																data-value="#E7D6DE"
																title=""
																aria-label="Twilight"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Twilight"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e79c9c;
																"
																data-event="foreColor"
																data-value="#E79C9C"
																title=""
																aria-label="Tonys Pink"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tonys Pink"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffc69c;
																"
																data-event="foreColor"
																data-value="#FFC69C"
																title=""
																aria-label="Peach Orange"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Peach Orange"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffe79c;
																"
																data-event="foreColor"
																data-value="#FFE79C"
																title=""
																aria-label="Cream Brulee"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cream Brulee"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #b5d6a5;
																"
																data-event="foreColor"
																data-value="#B5D6A5"
																title=""
																aria-label="Sprout"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Sprout"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #a5c6ce;
																"
																data-event="foreColor"
																data-value="#A5C6CE"
																title=""
																aria-label="Casper"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Casper"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9cc6ef;
																"
																data-event="foreColor"
																data-value="#9CC6EF"
																title=""
																aria-label="Perano"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Perano"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #b5a5d6;
																"
																data-event="foreColor"
																data-value="#B5A5D6"
																title=""
																aria-label="Cold Purple"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cold Purple"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #d6a5bd;
																"
																data-event="foreColor"
																data-value="#D6A5BD"
																title=""
																aria-label="Careys Pink"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Careys Pink"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e76363;
																"
																data-event="foreColor"
																data-value="#E76363"
																title=""
																aria-label="Mandy"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Mandy"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #f7ad6b;
																"
																data-event="foreColor"
																data-value="#F7AD6B"
																title=""
																aria-label="Rajah"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Rajah"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ffd663;
																"
																data-event="foreColor"
																data-value="#FFD663"
																title=""
																aria-label="Dandelion"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Dandelion"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #94bd7b;
																"
																data-event="foreColor"
																data-value="#94BD7B"
																title=""
																aria-label="Olivine"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Olivine"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #73a5ad;
																"
																data-event="foreColor"
																data-value="#73A5AD"
																title=""
																aria-label="Gulf Stream"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Gulf Stream"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #6badde;
																"
																data-event="foreColor"
																data-value="#6BADDE"
																title=""
																aria-label="Viking"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Viking"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #8c7bc6;
																"
																data-event="foreColor"
																data-value="#8C7BC6"
																title=""
																aria-label="Blue Marguerite"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Blue Marguerite"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #c67ba5;
																"
																data-event="foreColor"
																data-value="#C67BA5"
																title=""
																aria-label="Puce"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Puce"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #ce0000;
																"
																data-event="foreColor"
																data-value="#CE0000"
																title=""
																aria-label="Guardsman Red"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Guardsman Red"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #e79439;
																"
																data-event="foreColor"
																data-value="#E79439"
																title=""
																aria-label="Fire Bush"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Fire Bush"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #efc631;
																"
																data-event="foreColor"
																data-value="#EFC631"
																title=""
																aria-label="Golden Dream"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Golden Dream"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #6ba54a;
																"
																data-event="foreColor"
																data-value="#6BA54A"
																title=""
																aria-label="Chelsea Cucumber"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Chelsea Cucumber"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #4a7b8c;
																"
																data-event="foreColor"
																data-value="#4A7B8C"
																title=""
																aria-label="Smalt Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Smalt Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #3984c6;
																"
																data-event="foreColor"
																data-value="#3984C6"
																title=""
																aria-label="Boston Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Boston Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #634aa5;
																"
																data-event="foreColor"
																data-value="#634AA5"
																title=""
																aria-label="Butterfly Bush"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Butterfly Bush"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #a54a7b;
																"
																data-event="foreColor"
																data-value="#A54A7B"
																title=""
																aria-label="Cadillac"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cadillac"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #9c0000;
																"
																data-event="foreColor"
																data-value="#9C0000"
																title=""
																aria-label="Sangria"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Sangria"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #b56308;
																"
																data-event="foreColor"
																data-value="#B56308"
																title=""
																aria-label="Mai Tai"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Mai Tai"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #bd9400;
																"
																data-event="foreColor"
																data-value="#BD9400"
																title=""
																aria-label="Buddha Gold"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Buddha Gold"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #397b21;
																"
																data-event="foreColor"
																data-value="#397B21"
																title=""
																aria-label="Forest Green"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Forest Green"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #104a5a;
																"
																data-event="foreColor"
																data-value="#104A5A"
																title=""
																aria-label="Eden"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Eden"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #085294;
																"
																data-event="foreColor"
																data-value="#085294"
																title=""
																aria-label="Venice Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Venice Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #311873;
																"
																data-event="foreColor"
																data-value="#311873"
																title=""
																aria-label="Meteorite"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Meteorite"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #731842;
																"
																data-event="foreColor"
																data-value="#731842"
																title=""
																aria-label="Claret"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Claret"
															></button>
														</div>
														<div class="note-color-row">
															<button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #630000;
																"
																data-event="foreColor"
																data-value="#630000"
																title=""
																aria-label="Rosewood"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Rosewood"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #7b3900;
																"
																data-event="foreColor"
																data-value="#7B3900"
																title=""
																aria-label="Cinnamon"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Cinnamon"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #846300;
																"
																data-event="foreColor"
																data-value="#846300"
																title=""
																aria-label="Olive"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Olive"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #295218;
																"
																data-event="foreColor"
																data-value="#295218"
																title=""
																aria-label="Parsley"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Parsley"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #083139;
																"
																data-event="foreColor"
																data-value="#083139"
																title=""
																aria-label="Tiber"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Tiber"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #003163;
																"
																data-event="foreColor"
																data-value="#003163"
																title=""
																aria-label="Midnight Blue"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Midnight Blue"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #21104a;
																"
																data-event="foreColor"
																data-value="#21104A"
																title=""
																aria-label="Valentino"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Valentino"
															></button
															><button
																type="button"
																class="note-color-btn"
																style="
																	background-color: #4a1031;
																"
																data-event="foreColor"
																data-value="#4A1031"
																title=""
																aria-label="Loulou"
																data-toggle="button"
																tabindex="-1"
																data-original-title="Loulou"
															></button>
														</div>
													</div>
												</div>
												<div>
													<button
														type="button"
														class="note-color-select btn"
														data-event="openPalette"
														data-value="foreColorPicker"
													>
														Select
													</button>
													<input
														type="color"
														id="foreColorPicker"
														class="note-btn note-color-select-btn"
														value="#000000"
														data-event="foreColorPalette"
													/>
													<div
														class="note-holder-custom"
														id="foreColorPalette"
														data-event="foreColor"
													>
														<div class="note-color-palette">
															<div class="note-color-row">
																<button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button
																><button
																	type="button"
																	class="note-color-btn"
																	style="
																		background-color: #ffffff;
																	"
																	data-event="foreColor"
																	data-value="#FFFFFF"
																	title=""
																	aria-label="#FFFFFF"
																	data-toggle="button"
																	tabindex="-1"
																	data-original-title="#FFFFFF"
																></button>
															</div>
														</div>
													</div>
												</div>
											</div>
										</ul>
									</div>
								</div>
								<div class="note-btn-group btn-group note-para">
									<button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Unordered list (CTRL+SHIFT+NUM7)"
										data-original-title="Unordered list (CTRL+SHIFT+NUM7)"
									>
										<i class="note-icon-unorderedlist"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Ordered list (CTRL+SHIFT+NUM8)"
										data-original-title="Ordered list (CTRL+SHIFT+NUM8)"
									>
										<i class="note-icon-orderedlist"></i>
									</button>
									<div class="note-btn-group btn-group">
										<button
											type="button"
											class="note-btn btn btn-default btn-sm dropdown-toggle"
											role="button"
											tabindex="-1"
											data-toggle="dropdown"
											title=""
											aria-label="Paragraph"
											data-original-title="Paragraph"
										>
											<i class="note-icon-align-left"></i>
											<span class="note-icon-caret"></span>
										</button>
										<ul class="dropdown-menu" role="list">
											<div
												class="note-btn-group btn-group note-align"
											>
												<button
													type="button"
													class="note-btn btn btn-default btn-sm"
													role="button"
													tabindex="-1"
													title=""
													aria-label="Align left (CTRL+SHIFT+L)"
													data-original-title="Align left (CTRL+SHIFT+L)"
												>
													<i
														class="note-icon-align-left"
													></i></button
												><button
													type="button"
													class="note-btn btn btn-default btn-sm"
													role="button"
													tabindex="-1"
													title=""
													aria-label="Align center (CTRL+SHIFT+E)"
													data-original-title="Align center (CTRL+SHIFT+E)"
												>
													<i
														class="note-icon-align-center"
													></i></button
												><button
													type="button"
													class="note-btn btn btn-default btn-sm"
													role="button"
													tabindex="-1"
													title=""
													aria-label="Align right (CTRL+SHIFT+R)"
													data-original-title="Align right (CTRL+SHIFT+R)"
												>
													<i
														class="note-icon-align-right"
													></i></button
												><button
													type="button"
													class="note-btn btn btn-default btn-sm"
													role="button"
													tabindex="-1"
													title=""
													aria-label="Justify full (CTRL+SHIFT+J)"
													data-original-title="Justify full (CTRL+SHIFT+J)"
												>
													<i
														class="note-icon-align-justify"
													></i>
												</button>
											</div>
											<div
												class="note-btn-group btn-group note-list"
											>
												<button
													type="button"
													class="note-btn btn btn-default btn-sm"
													role="button"
													tabindex="-1"
													title=""
													aria-label="Outdent (CTRL+[)"
													data-original-title="Outdent (CTRL+[)"
												>
													<i
														class="note-icon-align-outdent"
													></i></button
												><button
													type="button"
													class="note-btn btn btn-default btn-sm"
													role="button"
													tabindex="-1"
													title=""
													aria-label="Indent (CTRL+])"
													data-original-title="Indent (CTRL+])"
												>
													<i class="note-icon-align-indent"></i>
												</button>
											</div>
										</ul>
									</div>
								</div>
								<div class="note-btn-group btn-group note-table">
									<div class="note-btn-group btn-group">
										<button
											type="button"
											class="note-btn btn btn-default btn-sm dropdown-toggle"
											role="button"
											tabindex="-1"
											data-toggle="dropdown"
											title=""
											aria-label="Table"
											data-original-title="Table"
										>
											<i class="note-icon-table"></i>
											<span class="note-icon-caret"></span>
										</button>
										<ul
											class="dropdown-menu note-table"
											role="list"
											aria-label="Table"
										>
											<div class="note-dimension-picker">
												<div
													class="note-dimension-picker-mousecatcher"
													data-event="insertTable"
													data-value="1x1"
													style="width: 10em; height: 10em;"
												></div>
												<div
													class="note-dimension-picker-highlighted"
												></div>
												<div
													class="note-dimension-picker-unhighlighted"
												></div>
											</div>
											<div class="note-dimension-display">
												1 x 1
											</div>
										</ul>
									</div>
								</div>
								<div class="note-btn-group btn-group note-insert">
									<button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Link (CTRL+K)"
										data-original-title="Link (CTRL+K)"
									>
										<i class="note-icon-link"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Picture"
										data-original-title="Picture"
									>
										<i class="note-icon-picture"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Video"
										data-original-title="Video"
									>
										<i class="note-icon-video"></i>
									</button>
								</div>
								<div class="note-btn-group btn-group note-view">
									<button
										type="button"
										class="note-btn btn btn-default btn-sm btn-fullscreen"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Full Screen"
										data-original-title="Full Screen"
									>
										<i class="note-icon-arrows-alt"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm btn-codeview"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Code View"
										data-original-title="Code View"
									>
										<i class="note-icon-code"></i></button
									><button
										type="button"
										class="note-btn btn btn-default btn-sm"
										role="button"
										tabindex="-1"
										title=""
										aria-label="Help"
										data-original-title="Help"
									>
										<i class="note-icon-question"></i>
									</button>
								</div>
							</div>
							<!-- <div class="note-editing-area">
								<div class="note-placeholder" style="display: block;">
									请输入文字
								</div>
								<div class="note-handle">
									<div
										class="note-control-selection"
										style="display: none;"
									>
										<div class="note-control-selection-bg"></div>
										<div
											class="note-control-holder note-control-nw"
										></div>
										<div
											class="note-control-holder note-control-ne"
										></div>
										<div
											class="note-control-holder note-control-sw"
										></div>
										<div
											class="note-control-sizing note-control-se"
										></div>
										<div class="note-control-selection-info"></div>
									</div>
								</div>
								<textarea
									class="note-codable"
									role="textbox"
									aria-multiline="true"
								></textarea>
								<div
									class="note-editable"
									contenteditable="true"
									role="textbox"
									aria-multiline="true"
									style="height: 180px;"
								></div>
							</div> -->
							<output
								class="note-status-output"
								aria-live="polite"
							></output>
							<div class="note-statusbar" role="status">
								<div
									class="note-resizebar"
									role="seperator"
									aria-orientation="horizontal"
									aria-label="Resize"
								>
									<div class="note-icon-bar"></div>
									<div class="note-icon-bar"></div>
									<div class="note-icon-bar"></div>
								</div>
							</div>
							<div
								class="modal link-dialog"
								style="display: none !important;"
								aria-hidden="false"
								tabindex="-1"
								role="dialog"
								aria-label="Insert Link"
							>
								<div class="modal-dialog">
									<div class="modal-content">
										<div class="modal-header">
											<button
												type="button"
												class="close"
												data-dismiss="modal"
												aria-label="Close"
												aria-hidden="true"
											>
												×
											</button>
											<h4 class="modal-title">Insert Link</h4>
										</div>
										<div class="modal-body">
											<div class="form-group note-form-group">
												<label class="note-form-label"
													>Text to display</label
												><input
													class="note-link-text form-control note-form-control note-input"
													type="text"
												/>
											</div>
											<div class="form-group note-form-group">
												<label class="note-form-label"
													>To what URL should this link
													go?</label
												><input
													class="note-link-url form-control note-form-control note-input"
													type="text"
													value="http://"
												/>
											</div>
											<div
												class="checkbox sn-checkbox-open-in-new-window"
											>
												<label>
													<input
														role="checkbox"
														type="checkbox"
														checked=""
														aria-checked="true"
													/>Open in new window</label
												>
											</div>
										</div>
										<div class="modal-footer">
											<input
												type="button"
												href="#"
												class="btn btn-primary note-btn note-btn-primary note-link-btn"
												value="Insert Link"
												disabled=""
											/>
										</div>
									</div>
								</div>
							</div>
							<div
								class="modal"
								style="display: none !important;"
								aria-hidden="false"
								tabindex="-1"
								role="dialog"
								aria-label="Insert Image"
							>
								<div class="modal-dialog">
									<div class="modal-content">
										<div class="modal-header">
											<button
												type="button"
												class="close"
												data-dismiss="modal"
												aria-label="Close"
												aria-hidden="true"
											>
												×
											</button>
											<h4 class="modal-title">Insert Image</h4>
										</div>
										<div class="modal-body">
											<div
												class="form-group note-form-group note-group-select-from-files"
											>
												<label class="note-form-label"
													>Select from files</label
												><input
													class="note-image-input note-form-control note-input"
													type="file"
													name="files"
													accept="image/*"
													multiple="multiple"
												/>
											</div>
											<div
												class="form-group note-group-image-url"
												style="overflow: auto;"
											>
												<label class="note-form-label"
													>Image URL</label
												><input
													class="note-image-url form-control note-form-control note-input col-md-12"
													type="text"
												/>
											</div>
										</div>
										<div class="modal-footer">
											<input
												type="button"
												href="#"
												class="btn btn-primary note-btn note-btn-primary note-image-btn"
												value="Insert Image"
												disabled=""
											/>
										</div>
									</div>
								</div>
							</div>
							<div
								class="modal"
								style="display: none !important;"
								aria-hidden="false"
								tabindex="-1"
								role="dialog"
								aria-label="Insert Video"
							>
								<div class="modal-dialog">
									<div class="modal-content">
										<div class="modal-header">
											<button
												type="button"
												class="close"
												data-dismiss="modal"
												aria-label="Close"
												aria-hidden="true"
											>
												×
											</button>
											<h4 class="modal-title">Insert Video</h4>
										</div>
										<div class="modal-body">
											<div
												class="form-group note-form-group row-fluid"
											>
												<label class="note-form-label"
													>Video URL
													<small class="text-muted"
														>(YouTube, Vimeo, Vine, Instagram,
														DailyMotion or Youku)</small
													></label
												><input
													class="note-video-url form-control note-form-control note-input"
													type="text"
												/>
											</div>
										</div>
										<div class="modal-footer">
											<input
												type="button"
												href="#"
												class="btn btn-primary note-btn note-btn-primary note-video-btn"
												value="Insert Video"
												disabled=""
											/>
										</div>
									</div>
								</div>
							</div>
							<div
								class="modal"
								style="display: none !important;"
								aria-hidden="false"
								tabindex="-1"
								role="dialog"
								aria-label="Help"
							>
								<div class="modal-dialog">
									<div class="modal-content">
										<div class="modal-header">
											<button
												type="button"
												class="close"
												data-dismiss="modal"
												aria-label="Close"
												aria-hidden="true"
											>
												×
											</button>
											<h4 class="modal-title">Help</h4>
										</div>
										<div
											class="modal-body"
											style="max-height: 300px; overflow: scroll;"
										>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>ENTER</kbd></label
											><span>Insert Paragraph</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+Z</kbd></label
											><span>Undoes the last command</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+Y</kbd></label
											><span>Redoes the last command</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>TAB</kbd></label
											><span>Tab</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>SHIFT+TAB</kbd></label
											><span>Untab</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+B</kbd></label
											><span>Set a bold style</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+I</kbd></label
											><span>Set a italic style</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+U</kbd></label
											><span>Set a underline style</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+S</kbd></label
											><span>Set a strikethrough style</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+BACKSLASH</kbd></label
											><span>Clean a style</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+L</kbd></label
											><span>Set left align</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+E</kbd></label
											><span>Set center align</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+R</kbd></label
											><span>Set right align</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+J</kbd></label
											><span>Set full align</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+NUM7</kbd></label
											><span>Toggle unordered list</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+SHIFT+NUM8</kbd></label
											><span>Toggle ordered list</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+LEFTBRACKET</kbd></label
											><span>Outdent on current paragraph</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+RIGHTBRACKET</kbd></label
											><span>Indent on current paragraph</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM0</kbd></label
											><span
												>Change current block's format as a
												paragraph(P tag)</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM1</kbd></label
											><span
												>Change current block's format as H1</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM2</kbd></label
											><span
												>Change current block's format as H2</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM3</kbd></label
											><span
												>Change current block's format as H3</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM4</kbd></label
											><span
												>Change current block's format as H4</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM5</kbd></label
											><span
												>Change current block's format as H5</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+NUM6</kbd></label
											><span
												>Change current block's format as H6</span
											>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+ENTER</kbd></label
											><span>Insert horizontal rule</span>
											<div class="help-list-item"></div>
											<label
												style="width: 180px; margin-right: 10px;"
												><kbd>CTRL+K</kbd></label
											><span>Show Link Dialog</span>
										</div>
										<div class="modal-footer">
											<p class="text-center">
												<a
													href="http://summernote.org/"
													target="_blank"
													>Summernote 0.8.11</a
												>
												Â·
												<a
													href="https://github.com/summernote/summernote"
													target="_blank"
													>Project</a
												>
												Â·
												<a
													href="https://github.com/summernote/summernote/issues"
													target="_blank"
													>Issues</a
												>
											</p>
										</div>
									</div>
								</div>
							</div>
						</div>
						<div class="edit_text_btn">
							<div class="edit_text_cancel">取消</div>
							<div class="edit_text_confirm">确认</div>
						</div>
					</div>
				</div>
			</div>
			<!--添加产品底部弹框-->
			<div id="pro_wrap" class="weui-popup__container">
				<div class="weui-popup__overlay"></div>
				<div class="weui-popup__modal pro_content">
					<div class="pro_slide_bar">
						<div class="pro_slide_ul"></div>
						<div class="close_con" @click="closeProModal">
							<img
								src="https://staticoss.bxdaka.com/static/images/close_pro.png"
								alt="关闭"
							/>
						</div>
					</div>
					<!--产品列表-->
					<div class="pro_wrapper">
						<div class="pro_content_inner"></div>
						<div class="weui-loadmore">
							<i class="weui-loading"></i>
							<span class="weui-loadmore__tips">正在加载</span>
						</div>
						<div class="no_more">没有更多了~</div>
					</div>
				</div>
			</div>
			<!--反馈图片弹框-->
			<div id="feed_popup" class="weui-popup__container">
				<div class="weui-popup__overlay"></div>
				<div class="weui-popup__modal feed_container">
					<div class="feed_title">文章含有以下敏感图片</div>
					<div class="feed_con clear"></div>
					<div class="feed_footer">
						<div class="feed_footer_l">
							<div class="feed_btn">识别有误反馈</div>
							<div class="feed_cancel hidden">取消</div>
						</div>
						<div class="feed_footer_r">
							<div class="back_edit">去修改</div>
							<div class="feed_submit hidden">提交反馈</div>
						</div>
					</div>
				</div>
			</div>
			<!--文章标题， 封面图， 描述-->
			<div class="article_title_wrap">
				<div class="article_title">
					官方回应来了！中科院90位博士集体离职研究所，他们是被挖走的...
				</div>
				<div class="article_title_other">
					<div class="article_title_des">书读一半，导师跑了</div>
					<van-uploader :after-read="afterRead1" :max-count="1">
						<div class="article_cover_img">
							<div class="opacity_cover">
								<img
									class="opacity_cover_img"
									src="https://staticoss.bxdaka.com/static/images/camera_icon.png"
									alt="相机"
								/>
								<span class="opacity_cover_text">点击更换</span>
							</div>
							<!-- <img
								class="inner_cover_img"
								src="http://static.bxdaka.com/article_upload_pic_cover_15430381595071881"
								alt="封面图"
							/> -->
							<img class="inner_cover_img" :src="imgUrl" alt="封面图" />
						</div>
					</van-uploader>
				</div>
			</div>
			<div class="edit_top">
				<div class="edit_add_wrap">
					<img
						src="https://staticoss.bxdaka.com/static/images/app15_tthk_create_jia.png"
						alt="增加"
					/>
				</div>
				<div class="edit_add_con_wrap hidden">
					<div class="edit_add_con">
						<div class="edit_btn_item_t" @click="editAddTopText">
							<div class="edit_btn_txt_icon_t"></div>
							<span class="edit_btn_txt">文字</span>
						</div>
						<van-uploader :after-read="afterRead2" :max-count="1">
							<div class="edit_btn_item_t">
								<div
									class="edit_btn_img_icon_t"
									@onclick="addTopImg"
								></div>
								<span class="edit_btn_txt">图片</span>
							</div>
						</van-uploader>
					</div>
				</div>
			</div>
			<!--文章内容-->
			<!--底部按钮-->
			<!-- <div class="art-content">
				<span>水电费水电费是的舒舒服服</span>
			</div> -->
			<div class="art-content">
				<h2
					style="
						font-family: -apple-system-font, system-ui, 'Helvetica Neue',
							'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei UI',
							'Microsoft YaHei', Arial, sans-serif;
						line-height: 1.2;
						color: rgba(0, 0, 0, 0.85);
						letter-spacing: 0.544px;
						white-space: normal;
						background-color: rgb(255, 255, 255);
					"
					data-mpa-powered-by="yiban.io"
					class="other-section"
				>
					<p
						style="
							letter-spacing: 0.544px;
							text-align: center;
							margin-left: 16px;
							margin-right: 16px;
						"
						class="other-section"
					>
						<span
							mpa-from-tpl="t"
							style="
								font-weight: bolder;
								letter-spacing: 0.544px;
								font-size: 12px;
								color: rgb(136, 136, 136);
							"
							class="other-section"
							>点击“</span
						><span
							style="
								color: rgb(0, 82, 255);
								font-weight: bolder;
								letter-spacing: 0.544px;
								font-size: 12px;
							"
							class="other-section"
							>开发者技术前线</span
						><span
							mpa-from-tpl="t"
							style="
								font-weight: bolder;
								letter-spacing: 0.544px;
								font-size: 12px;
								color: rgb(136, 136, 136);
							"
							class="other-section"
							>”，选择“星标🔝”</span
						>
					</p>
					<section
						style="
							letter-spacing: 0.544px;
							text-align: center;
							margin-left: 16px;
							margin-right: 16px;
						"
						class="other-section"
					>
						<span
							mpa-from-tpl="t"
							style="
								font-weight: bolder;
								letter-spacing: 0.544px;
								font-size: 12px;
								color: rgb(136, 136, 136);
							"
							class="other-section"
							>在看|星标|留言,&nbsp; 真爱</span
						>
					</section>
				</h2>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<p class="other-section">
					<img
						data-cropselx1="0"
						data-cropselx2="578"
						data-cropsely1="0"
						data-cropsely2="298"
						data-ratio="0.7494623655913979"
						data-src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_png/Uic0S1r5o6OuDYwwKibQeUJUGJrfHFJaUtKmGShYZ6E0hQrMNNNM2eul71UbnjKia9uCjktcibC5lU6fic0oTiaNfZpg/640"
						data-type="png"
						data-w="930"
						height="604"
						style="
							white-space: normal;
							border-border-style: initial;
							border-color: initial;
							width: 578px;
							display: block;
							height: 433px;
						"
						width="929"
						src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_png/Uic0S1r5o6OuDYwwKibQeUJUGJrfHFJaUtKmGShYZ6E0hQrMNNNM2eul71UbnjKia9uCjktcibC5lU6fic0oTiaNfZpg/640"
						data-original-src="mmbiz.qpic.cn/mmbiz_png/Uic0S1r5o6OuDYwwKibQeUJUGJrfHFJaUtKmGShYZ6E0hQrMNNNM2eul71UbnjKia9uCjktcibC5lU6fic0oTiaNfZpg/640"
					/>
				</p>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
						text-align: right;
					"
					class="other-section"
				>
					<span style="font-size: 14px; color: rgb(136, 136, 136);"
						>开发者技术前线 可可整理<br
					/></span>
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span
						style="
							color: rgb(74, 74, 74);
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
							font-size: 16px;
							letter-spacing: 0.544px;
							white-space: pre-line;
							background-color: rgb(255, 255, 255);
						"
						>7月15日，有报道称，近期，中科院合肥物质科学研究院下属的核能安全技术研究所（以下简称“核所”）多名科研人员集体出走，其中大多数是博士毕业，并拥有事业编制。这在中科院系统内引起广泛关注<br
					/></span>
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span
						style="
							color: rgb(74, 74, 74);
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
							font-size: 16px;
							letter-spacing: 0.544px;
							white-space: pre-line;
							background-color: rgb(255, 255, 255);
						"
						>据称，集体辞职事件的导火索，是院方强制为核所更换保安，核所科研人员认为自身权益被侵犯。</span
					>
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span
						style="
							color: rgb(74, 74, 74);
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
							font-size: 16px;
							letter-spacing: 0.544px;
							white-space: pre-line;
							background-color: rgb(255, 255, 255);
						"
						>近日根据有关消息显示，位于合肥的中科院物质科学研究所有90名科研人员辞职，根据报道可能与科研人员工资有关。具体原因目前仍然在调查跟进中。</span
					>
				</section>
				<p
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</p>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span
						style="
							color: rgb(74, 74, 74);
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
							font-size: 16px;
							letter-spacing: 0.544px;
							white-space: pre-line;
							background-color: rgb(255, 255, 255);
						"
						>来自于sogo百科关于该研究所的具体介绍：中国科学院合肥物质科学研究院应用技术研究所，聚焦相关应用技术领域的核心技术，通过集中合肥研究院相关优势资源、聚集优秀人才队伍，在先进材料技术、智能控制技术、光电子技术、新能源技术、生物技术等应用技术方向开展技术攻关，形成具有重要创新价值的产业适用技术；构筑高水平技术创新人才培养基地；探索以市场需求为导向的科研体制和机制。</span
					><span
						style="
							text-align: center;
							font-family: mp-quote, -apple-system-font, BlinkMacSystemFont,
								'Helvetica Neue', 'PingFang SC', 'Hiragino Sans GB',
								'Microsoft YaHei UI', 'Microsoft YaHei', Arial, sans-serif;
							font-size: 17px;
						"
					></span>
				</section>
				<p class="other-section"><br /></p>
				<p class="other-section"><br /></p>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span
						style="
							color: rgb(74, 74, 74);
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
							font-size: 16px;
							letter-spacing: 0.544px;
							white-space: pre-line;
							background-color: rgb(255, 255, 255);
						"
						>从介绍中我们可以看出这个研究所聚焦的是高科技高水平的先进技术。究竟为何导致90多名博士学位的科研人才集体离职呢？作为考研行业工作者其实最不想看见的就是这些，科研事业是我们每一个受过高等教育的人所向往的工作，也是我们科教兴国的根本。</span
					>
				</section>
				<p class="other-section">
					<img
						data-ratio="1.3359375"
						data-type="jpeg"
						data-w="640"
						data-src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPtNsBZUBFMO4eQpbmyyYdKcWttVq9VWnRlZZFpXK5lg4aA7ohvBojNg/640"
						style="
							border-border-style: initial;
							border-color: initial;
							width: 600px;
							display: block;
						"
						src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPtNsBZUBFMO4eQpbmyyYdKcWttVq9VWnRlZZFpXK5lg4aA7ohvBojNg/640"
						data-original-src="mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPtNsBZUBFMO4eQpbmyyYdKcWttVq9VWnRlZZFpXK5lg4aA7ohvBojNg/640"
					/>
				</p>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span
						style="
							color: rgb(74, 74, 74);
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
							font-size: 16px;
							letter-spacing: 0.544px;
							white-space: pre-line;
							background-color: rgb(255, 255, 255);
						"
						>在国家大力支持科研事业的关键时刻，为何出现如此大规模高学历人才的辞职？这背后的情况值得我们去研究调查，在改革的同时难道不应该考虑到和保护科研人员的利益吗？我们不仅要培养人才，也要留得住人才才可以！</span
					>
				</section>
				<p class="other-section">
					<img
						data-ratio="1.6859375"
						data-type="jpeg"
						data-w="640"
						data-src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPzJHQENumUgHgCc9ZPlQBASkvLHYtcQ2mobQVt8B4quowE2L9IiajDkQ/640"
						style="
							border-border-style: initial;
							border-color: initial;
							width: 600px;
							display: block;
						"
						src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPzJHQENumUgHgCc9ZPlQBASkvLHYtcQ2mobQVt8B4quowE2L9IiajDkQ/640"
						data-original-src="mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPzJHQENumUgHgCc9ZPlQBASkvLHYtcQ2mobQVt8B4quowE2L9IiajDkQ/640"
					/>
				</p>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					这个现象到底正常与否大家心里应该都有自己的判断，一两个离职实属正常，但大批次的编制内人才集体离职背后难道没有原因吗？网络上大部分网友都认为这件事不简单，应该有一些共同的原因才使他们集体离职。
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					这种集体出走的原因不可能是简单的缺项目、少经费这么简单。
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					7月16日，有媒体报道称，中国科学院合肥物质科学研究院90多名科研人员离职。报道引用一名内部人士的表述称，离职人员集中于合肥研究院核能安全技术研究所，其中大多数是博士毕业，并拥有事业编制。时间均在今年年内，离职原因似与待遇并无直接关联。<br />
				</section>
				<section
					style="
						color: rgb(64, 64, 64);
						font-family: 'Microsoft Yahei';
						font-size: 18px;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<img
						data-ratio="0.5569422776911076"
						data-type="jpeg"
						data-w="641"
						data-src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPN4YUTic0Fibwk4ib46oxpAPLg2YZ2E2SDicMwFgQ21JKayLziaaxsNh6E8g/640"
						style="
							border-width: initial;
							border-style: none;
							border-color: initial;
							width: 641px;
							height: 357px;
						"
						src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPN4YUTic0Fibwk4ib46oxpAPLg2YZ2E2SDicMwFgQ21JKayLziaaxsNh6E8g/640"
						data-original-src="mmbiz.qpic.cn/mmbiz_jpg/Uic0S1r5o6OuE07TtgnZXUVibXUrJLibkxPN4YUTic0Fibwk4ib46oxpAPLg2YZ2E2SDicMwFgQ21JKayLziaaxsNh6E8g/640"
					/>
				</section>
				<section
					style="
						margin-top: 26px;
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<span style="color: rgb(0, 128, 255);"
						><strong>研究所回应集体离职 被挖走的！</strong></span
					>
				</section>
				<section class="other-section"></section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					据了解，核安全所是中国科学院合肥物质科学研究院下属研究所。该研究所一名负责离职管理的工作人员称，90多名科研人员于6月份集体向该研究院提出离职，“<strong>他们都是自愿离职的，现离职手续都已经办完。</strong>”
				</section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				></section>
				<section
					style="
						font-size: 16px;
						line-height: 24px;
						font-family: arial;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					前述工作人员透露，这90多名科研人员确实是被挖走的，但离职属于正常人员流动。
				</section>
				<section
					style="line-height: 1.75em; margin-left: 16px; margin-right: 16px;"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						white-space: normal;
						line-height: 2em;
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						white-space: normal;
						line-height: 2em;
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				></section>
				<section
					style="margin-left: 16px; margin-right: 16px;"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						padding-top: 8px;
						padding-bottom: 8px;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						text-align: left;
						widows: 1;
						caret-color: rgb(255, 0, 0);
						color: rgb(0, 0, 0);
						font-family: PingFangSC-Light;
						line-height: 1.75;
						letter-spacing: 0.1em;
						font-size: 15px;
						word-spacing: 0.1em;
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					&nbsp;最后给读者整理了一份大厂面试真题，需要的可扫码加我微信获取。<br />
				</section>
				<section
					style="
						letter-spacing: 0.544px;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						font-size: 16px;
						widows: 1;
						word-spacing: 2px;
						caret-color: rgb(255, 0, 0);
						color: rgb(0, 0, 0);
						font-family: PingFangSC-Light;
						text-align: center;
						margin-left: 16px;
						margin-right: 16px;
					"
					class="other-section"
				>
					<img
						class="rich_pages"
						data-ratio="1.0527777777777778"
						data-s="300,640"
						data-type="png"
						data-w="1080"
						height="1137"
						data-src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_png/Uic0S1r5o6OvViaHqykkOHyzTaCkmDSYFXexIrrkBCG4ghiandLVbtyV2v79BslCNrVnqXax3d8icIx6ndXukrYiaPw/640"
						style="
							vertical-align: middle;
							border-style: none;
							box-sizing: border-box !important;
							visibility: visible !important;
							width: 575px !important;
						"
						width="1080"
						src="http://static.bxdaka.com/bxdk_res/mmbiz.qpic.cn/mmbiz_png/Uic0S1r5o6OvViaHqykkOHyzTaCkmDSYFXexIrrkBCG4ghiandLVbtyV2v79BslCNrVnqXax3d8icIx6ndXukrYiaPw/640"
						data-original-src="mmbiz.qpic.cn/mmbiz_png/Uic0S1r5o6OvViaHqykkOHyzTaCkmDSYFXexIrrkBCG4ghiandLVbtyV2v79BslCNrVnqXax3d8icIx6ndXukrYiaPw/640"
					/>
				</section>
				<section
					style="margin-left: 16px; margin-right: 16px;"
					class="other-section"
				>
					<br />
				</section>
				<section
					style="
						font-family: -apple-system-font, system-ui, 'Helvetica Neue',
							'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei UI',
							'Microsoft YaHei', Arial, sans-serif;
						letter-spacing: 0.544px;
						white-space: normal;
						background-color: rgb(255, 255, 255);
						font-size: 16px;
						text-align: left;
						widows: 1;
						word-spacing: 2px;
						caret-color: rgb(255, 0, 0);
						color: rgb(0, 0, 0);
					"
					class="other-section"
				>
					<section class="other-section">
						<section
							data-role="outer"
							label="Powered by 135editor.com"
							class="other-section"
						>
							<section data-role="paragraph">
								<pre
									style=""
								><section><section style="margin-left: 16px;margin-right: 16px;"><br></section><section style="margin-left: 16px;margin-right: 16px;"><span style="font-size: 15px;">前线推出学习交流群，加群一定要备注：</span></section><section style="margin-left: 16px;margin-right: 16px;"><span style="font-size: 15px;color: rgb(0, 82, 255);">研究/工作方向 地点 学校/公司 昵称（如前端 上海 上交 可可）</span></section><section style="margin-left: 16px;margin-right: 16px;"><span style="font-size: 15px;">根据格式备注，可更快被通过且邀请进群，领取一份专属学习礼包</span></section><section data-mpa-template="t" mpa-from-tpl="t"><section data-mpa-template="t" mpa-from-tpl="t"><section data-recommend-type="list-title" data-mpa-template="t" data-mid="" data-from="yb-recommend" mpa-from-tpl="t"><section data-mid="" mpa-from-tpl="t"><section data-mid="" mpa-from-tpl="t"><section data-mid="" mpa-from-tpl="t"><h1 style="font-family: inherit;line-height: 1.2;color: rgba(0, 0, 0, 0.85);"><section data-mpa-template="t" mpa-from-tpl="t" style="letter-spacing: 0.544px;"><section style="letter-spacing: 0.544px;"><section powered-by="xiumi.us"><section><section><section powered-by="xiumi.us"><ul class="list-paddingleft-2" style="width: 577.422px;margin-left: 16px;margin-right: 16px;"><p style="text-align: center;"><br></p><p style="text-align: center;"></p></ul></section></section></section></section></section></section><section style="margin: 15px 16px;letter-spacing: 0.544px;white-space: pre-line;line-height: 30px;color: rgb(74, 74, 74);font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;text-align: center;"><span style="font-weight: bolder;">扫码加我微信进群，内推和技术交流，大佬们零距离</span></section></h1></section></section></section></section></section></section></section></pre>
							</section>
						</section>
					</section>
				</section>
				<section
					style="
						font-family: -apple-system-font, system-ui, 'Helvetica Neue',
							'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei UI',
							'Microsoft YaHei', Arial, sans-serif;
						white-space: normal;
						font-size: 15px;
						color: rgb(62, 62, 62);
						line-height: 1.8;
						word-spacing: 2px;
						letter-spacing: 2px;
					"
					class="other-section"
				>
					<section
						style="
							color: rgb(63, 63, 63);
							font-size: 16px;
							font-family: Avenir, -apple-system-font, 微软雅黑, sans-serif;
						"
						class="other-section"
					>
						<section
							style="
								font-family: -apple-system-font, system-ui,
									'Helvetica Neue', 'PingFang SC', 'Hiragino Sans GB',
									'Microsoft YaHei UI', 'Microsoft YaHei', Arial,
									sans-serif;
								letter-spacing: 0.544px;
							"
							class="other-section"
						>
							<section>
								<section
									style="letter-spacing: 0.544px; text-align: center;"
								>
									<section
										powered-by="xiumi.us"
										style="
											margin-top: 15px;
											margin-bottom: 25px;
											opacity: 0.8;
										"
									>
										<section>
											<section>
												<section style="letter-spacing: 0.544px;">
													<section
														style="
															letter-spacing: 0.544px;
															line-height: 27.2px;
														"
													>
														<section>
															<section
																style="
																	letter-spacing: 0.544px;
																	border-border-style: none;
																	border-color: initial;
																	z-index: 0;
																	color: rgb(0, 0, 0);
																	font-family: 微软雅黑;
																	text-align: start;
																	caret-color: rgb(
																		255,
																		0,
																		0
																	);
																	line-height: 1.75em;
																	margin-left: 16px;
																	margin-right: 16px;
																	outline: none 0px !important;
																"
															>
																<section
																	style="
																		display: flex;
																		justify-content: flex-end;
																		align-items: center;
																		outline: none 0px !important;
																	"
																>
																	<section
																		style="
																			margin-left: 6px;
																			letter-spacing: 0.544px;
																			background-color: rgb(
																				255,
																				255,
																				255
																			);
																			width: 28px;
																			outline: none
																				0px !important;
																		"
																	></section>
																	<section
																		style="
																			padding: 4px
																				15px 3px;
																			display: flex;
																			letter-spacing: 0.544px;
																			background-color: rgb(
																				255,
																				255,
																				255
																			);
																			border-width: 1px;
																			border-style: solid;
																			border-color: rgb(
																				51,
																				51,
																				51
																			);
																			border-radius: 20px;
																			justify-content: center;
																			align-items: center;
																			outline: none
																				0px !important;
																		"
																	>
																		<section
																			style="
																				width: 12px;
																				outline: none
																					0px !important;
																			"
																		></section>
																		<section
																			data-brushtype="text"
																			style="
																				padding-left: 5px;
																				color: rgb(
																					51,
																					51,
																					51
																				);
																				letter-spacing: 1.5px;
																				outline: none
																					0px !important;
																			"
																		>
																			<span
																				style="
																					color: rgb(
																						0,
																						82,
																						255
																					);
																					letter-spacing: 1px;
																					font-size: 13px;
																					font-weight: bolder;
																				"
																				>好文点个在看吧！</span
																			>
																		</section>
																		<p><br /></p>
																	</section>
																</section>
															</section>
														</section>
													</section>
												</section>
											</section>
										</section>
									</section>
								</section>
							</section>
						</section>
					</section>
				</section>
			</div>
			<div class="footer">
				<div class="footer_l" @click="cancelDelete">撤销删除</div>
				<div class="footer_r" id="save_article">保存</div>
			</div>
			<div class="footer_bar"></div>
		</div>
	</div>
</template>

<script>
wx.config({
	debug: false,
	appId: 'wxc2b659968ac6997b',
	timestamp: '1595071973',
	nonceStr: 'P6MNjb3fIcqyTmfJ',
	signature: 'c8784cc45431f73c5a53949e6aa060afe33bbf85',
	jsApiList: ['checkJsApi', 'chooseImage', 'uploadImage', 'hideMenuItems']
})
wx.ready(function() {
	wx.hideMenuItems({
		menuList: [
			'menuItem:share:timeline',
			'menuItem:share:appMessage',
			'menuItem:share:weiboApp',
			'menuItem:share:qq',
			'menuItem:share:QZone'
		]
	})
})
$(function() {
	FastClick.attach(document.body)
})
var appId = 47
var editTextStatus = 1 // 1为顶部添加文本   2 添加文本    3 编辑文本   4 编辑标题
var isAddTop = false // 是否是在顶部添加图片
var uid = '2w3zWq2UuudRB'
var avatar_url = 'http://static.bxdaka.com/user_avatar_20200707_5f03dbd508bf1.jpg'
var nickname = '%E5%8B%87%E5%BE%80%E7%9B%B4%E5%89%8D'
nickname = decodeURIComponent(nickname)
var pageIndex = 0 // 产品列表的页码数
var loading = false //状态标记
// 险种公司
var companyArr = []
// 已删除元素
var revoke_arr = []
var del_num = 0
var article_des = decodeURIComponent(
	'%E4%B9%A6%E8%AF%BB%E4%B8%80%E5%8D%8A%EF%BC%8C%E5%AF%BC%E5%B8%88%E8%B7%91%E4%BA%86'
)
var article_title = decodeURIComponent(
	'%E5%AE%98%E6%96%B9%E5%9B%9E%E5%BA%94%E6%9D%A5%E4%BA%86%EF%BC%81%E4%B8%AD%E7%A7%91%E9%99%A290%E4%BD%8D%E5%8D%9A%E5%A3%AB%E9%9B%86%E4%BD%93%E7%A6%BB%E8%81%8C%E7%A0%94%E7%A9%B6%E6%89%80%EF%BC%8C%E4%BB%96%E4%BB%AC%E6%98%AF%E8%A2%AB%E6%8C%96%E8%B5%B0%E7%9A%84...'
)
var isShowedNotice = localStorage.getItem('isShowedNotice')
var cmpyArr = '[]'
try {
	companyArr = JSON.parse(cmpyArr)
} catch (e) {
	alert('险种公司获取失败')
}
var curCompanyId = companyArr.length > 0 ? companyArr[0].company_id : '' // 当前点击的公司
var article_cover_media_id = ''
function articleEventListener() {
	$('.art-content')
		.children()
		.on('click', function(e) {
			console.warn(
				'点击任何地方',
				$(e.target)
					.parent()
					.is('.van-uploader__input-wrapper')
			)
			var nodeName = e.target.nodeName.toLowerCase()
			console.log(22, nodeName)
			if (
				$(e.target)
					.parents()
					.is('.art_section_edit') ||
				$(e.target).hasClass('iframe_div') ||
				$(e.target)
					.parents()
					.is('._135editor') ||
				$(e.target).hasClass('_135editor') ||
				$(e.target).hasClass('_iframe_editor')
			) {
				if (
					$(e.target)
						.parent()
						.is('.van-uploader__input-wrapper')
				) {
					return true
				} else {
					return false
				}
			}
			if (
				nodeName == 'img' ||
				nodeName == 'gift' ||
				nodeName == 'video' ||
				nodeName == 'audio'
			) {
				$('.edit_edit_btn').hide()
			} else {
				$('.edit_edit_btn').show()
			}
			// 删除占位元素
			$('._holder').remove()
			$('.art_section_edit').removeClass('hidden')
			// $('.edit_add_con_wrap').hide();
			$('.art-section').css('margin-bottom', '30px')
			$('.cur_edit_con')
				.closest('.art-section')
				.removeClass('padding_none')
			$('.cur_edit_con').removeClass('cur_edit_con')
			$('.art-content')
				.find('.cur_art_section')
				.removeClass('cur_art_section')
			$(e.target).addClass('cur_edit_con')
			$('.cur_edit_con')
				.closest('.art-section')
				.addClass('padding_none')
			$('.cur_edit_con').after($('.art_section_edit'))
			// 如果当前修改的是art-section
			if ($('.cur_edit_con').hasClass('art-section')) {
				$('.cur_edit_con').css('margin-bottom', '0')
				$('.art_section_edit').css('margin-bottom', '30px')
			}
			scrollToEl()
		})
}
// 滚动到指定位置
function scrollToEl(id) {
	var __total =
		$('.cur_edit_con').offset().top +
		$('.cur_edit_con').height() +
		$('.art_section_edit').height()
	var __height = $(window).scrollTop() + $(window).height() - $('.footer').height()
	if (__total < __height) {
		return
	}
	$('html, body').animate(
		{
			scrollTop: $(window).scrollTop() + __total - __height + 30
		},
		200
	)
}
// 是否显示文章摘要
function checkArticleDes() {
	article_des
		? $('.article_title_des').text(article_des)
		: $('.article_title_des').text(article_title)
}
// 获取险种
function getInsureList(companyId, pageIndex) {
	$('.pro_wrapper .weui-loadmore').show()
	$.ajax({
		url: '/index.php/Index/tthk/getProducts',
		type: 'post',
		data: { companyId: companyId, pageIndex: pageIndex },
		dataType: 'json',
		success: function(res) {
			// 获取产品列表
			var proList = res.list
			var _html = ''
			loading = false
			if (res.code == 2) {
				$('.pro_wrapper .weui-loadmore').hide()
				$('.no_more').show()
				return
			}
			for (var i = 0; i < proList.length; i++) {
				var features = '' // 产品描述
				if (proList[i].features) {
					proList[i].features = proList[i].features
						.replace(/&lt;/g, '<')
						.replace(/&gt;/g, '>')
						.replace(/&amp;/g, '&')
						.replace(/&quot;/g, '"')
						.replace(/&apos;/g, "'")
					features = proList[i].features
				} else {
					features = '专注保险保障本质，为您量身定制专属险种。'
				}
				_html +=
					'<div class="pro_list_con clear" data-risk_id="' +
					proList[i].product_id +
					'" data-link="/index.php/Index/Ad/productDetail/product_id/' +
					proList[i].product_id +
					'/uid/' +
					uid +
					'" data-risk_title="' +
					proList[i].product_name +
					'" data-risk_cover="' +
					proList[i].product_thumb_img_url +
					'" data-features_info="' +
					features +
					'">' +
					'<img src="' +
					proList[i].product_thumb_img_url +
					'" alt="产品图">' +
					'<div class="pro_list_info">' +
					'<p class="pro_list_title">' +
					proList[i].product_name +
					'</p>' +
					'<p class="pro_list_des">' +
					features +
					'</p>' +
					'</div>' +
					'</div>'
			}
			$('.pro_content_inner').append(_html)
			if ($('.pro_content_inner').html() != '') {
				$('.add_pro_btn').removeClass('hidden')
			} else {
				$('.add_pro_btn').addClass('hidden')
			}
			// 插入产品  为产品添加点击事件
			insertPro()
			$('.pro_wrapper .weui-loadmore').hide()
		}
	})
}
// 插入产品
function insertPro() {
	$('.pro_content_inner .pro_list_con').on('click', function(e) {
		e.stopPropagation()
		var risk_id = $(this).data('risk_id')
		var risk_detail_link = $(this).data('link')
		var risk_cover = $(this).data('risk_cover')
		var risk_title = $(this).data('risk_title')
		var risk_features = $(this).data('features_info')
		var _html = ''
		_html +=
			'<div class="art-section-new product-section" style="padding-bottom:46px;">'
		_html += '<a href="javascript:void(0);" data-href="' + risk_detail_link + '">'
		_html += '<div class="product-info">'
		_html += '<img src="' + risk_cover + '" />'
		_html += '<h3>' + risk_title + '</h3>'
		if (risk_features) {
			_html += '<div class="cont">' + risk_features + '</div>'
		} else {
			_html += '<div class="cont">专注保险保障本质，为您量身定制专属险种。</div>'
		}
		_html += '</div>'
		_html += '<div class="hr scale-half product-brd-line hidden"></div>'
		_html += '<div class="consult-column hidden">'
		_html += '<img src="' + avatar_url + '" />'
		_html += '<i>' + nickname.substring(0, 6) + '</i>'
		_html += '<span>咨询我>></span>'
		_html += '</div>'
		_html += '</a>'
		_html += '</div>'
		if (isAddTop) {
			$('.art-content').prepend(_html)
		} else {
			if ($('.cur_edit_con').closest('.art-section').length) {
				// 旧版之前文章的div
				$('.cur_edit_con')
					.closest('.art-section')
					.addClass('cur_art_section')
				$('.cur_art_section')
					.next()
					.hasClass('art_section_edit')
					? $('.art_section_edit').after(_html)
					: $('.cur_art_section').after(_html)
			} else {
				$('.art_section_edit').after(_html)
			}
			// else if ($('.cur_edit_con').closest('.art-section-new').length) {
			//   // 新版新加的段落，图片，产品都会是art-section-new的类
			//   $('.cur_edit_con').closest('.art-section-new').addClass('cur_art_section');
			//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
			// } else if ($('.cur_edit_con').closest('._135editor').length) {
			//   // 这个是135编辑器的类
			//   $('.cur_edit_con').closest('._135editor').addClass('cur_art_section');
			//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
			// } else if ($('.cur_edit_con').closest('.other-section').length) {
			//   // 其他文章的情况
			//   $('.cur_edit_con').closest('.other-section').addClass('cur_art_section');
			//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
			// }
		}
		$.toast('插入成功', 'text')
		// 重置数据
		isAddTop = false
		$('.edit_add_con_wrap').addClass('hidden')
		// articleEventListener();
		$.closePopup()
		// 释放
		stopBodyScroll(false)
	})
}
// 禁止body滚动
function stopBodyScroll(isFixed) {
	if (isFixed) {
		$('body, html').css({
			overflow: 'hidden'
		})
	} else {
		$('body, html').css({
			overflow: 'auto'
		})
	}
}
export default {
	data() {
		return {
			imgUrl: 'http://static.bxdaka.com/article_upload_pic_cover_15430381595071881'
		}
	},
	mounted() {
		$(document).ready(function() {
			// 编辑文章提示
			if (isShowedNotice) {
				$('.edit_notice_wrap').addClass('hidden')
			} else {
				$('.edit_notice_wrap').removeClass('hidden')
			}
			$('.edit_notice_wrap .no_notice').click(function() {
				localStorage.setItem('isShowedNotice', true)
				$('.edit_notice_wrap').addClass('hidden')
			})
			$('.edit_notice_wrap .notice_known').click(function() {
				$('.edit_notice_wrap').addClass('hidden')
			})
			$('.edit_notice_wrap').on('touchmove', function(e) {
				e.preventDefault()
			})
			// 文章摘要
			checkArticleDes()
			// $('#summernote').summernote();
			// 富文本编辑器
			$('#summernote').summernote({
				placeholder: '请输入文字',
				tabsize: 2,
				height: 200
			})
			//播放音频
			var audio_controls = $('audio').attr('controls')
			var weixinAudioObj = $('.weixinAudio').weixinAudio()
			if (!audio_controls) {
				$('audio').attr('controls', 'controls')
			}
			// 添加单一播放的逻辑
			$('.weixinAudio').on('click', function(event) {
				var currentIndex = $(this).attr('data-index')
				// 遍历所有对象，找到非当前点击，执行pause()方法;
				$.each(weixinAudioObj, function(i, el) {
					if (i != 'weixinAudio' + currentIndex) {
						el.pause()
					}
				})
			})
			// 初始化富文本
			$('#summernote').summernote('code', '')
			// 为没有art-section的标签加上art-section   加三层
			$('.art-content')
				.children()
				.each(function(index) {
					if (
						!$(this).hasClass('other-section') &&
						!$(this).hasClass('_135editor') &&
						!$(this).hasClass('art-section')
					) {
						// 如果不存在
						var _this = this
						$(_this).addClass('other-section')
						if ($(_this).find('section').length > 0) {
							$(_this)
								.children()
								.each(function() {
									var _this2 = this
									if (
										!$(_this2).hasClass('other-section') &&
										!$(_this2).hasClass('_135editor') &&
										!$(_this2).hasClass('art-section')
									) {
										$(_this2).addClass('other-section')
									}
									if ($(_this2).children().length > 0) {
										$(_this2)
											.children()
											.each(function() {
												if (
													!$(this).hasClass('other-section') &&
													!$(this).hasClass('_135editor') &&
													!$(this).hasClass('art-section')
												) {
													$(this).addClass('other-section')
												}
											})
									}
								})
						}
					}
				})
			// $('.art-section').each(function (index, el) {
			//   if ($(this).find('iframe').length) {
			//     var iframeWidth = $(this).find('iframe').width();
			//     var iframeHeight = $(this).find('iframe').height();
			//     $(this).css('position', 'relative');
			//     $(this).prepend('<div class="iframe_div" style="position: absolute; width: ' + iframeWidth + 'px; height: ' + iframeHeight + 'px;z-index: 8;"></div>')
			//   }
			// });
			// 设置编辑框的宽度为设备宽度
			$('.art_section_edit').width(document.body.clientWidth - 20)
			// 135编辑器  && 其他文章的iframe video处理
			$('iframe')
				.parent()
				.addClass('__video_wrap')
			$('video')
				.parent()
				.addClass('__video_wrap')
			$('.__video_wrap').each(function(index, el) {
				var iframeWidth = $(this)
					.find('iframe')
					.width()
				var iframeHeight = $(this)
					.find('iframe')
					.height()
				$(this).css('position', 'relative')
				$(this).prepend(
					'<div class="iframe_div" style="position: absolute; width: ' +
						iframeWidth +
						'px; height: ' +
						iframeHeight +
						'px;z-index: 8;"></div>'
				)
			})
			// 135编辑器
			$('._135editor').on('click', function(e) {
				if ($(e.currentTarget).hasClass('cur_edit_con')) {
					return
				}
				// 删除占位元素
				$('._holder').remove()
				$('.edit_edit_btn').show()
				$('.art_section_edit').removeClass('hidden')
				$('.cur_edit_con').removeClass('cur_edit_con')
				$(this).addClass('cur_edit_con')
				$(this).after($('.art_section_edit'))
			})
			$('.art-section-new').on('click', function(e) {
				if ($(e.currentTarget).hasClass('cur_edit_con')) {
					return
				}
				// 删除占位元素
				$('._holder').remove()
				$('.edit_edit_btn').show()
				$('.art_section_edit').removeClass('hidden')
				$('.cur_edit_con')
					.closest('.art-section')
					.removeClass('padding_none')
				$('.cur_edit_con').removeClass('cur_edit_con')
				$(this).addClass('cur_edit_con')
				$(this).after($('.art_section_edit'))
			})
			// 旧的文章编辑的iframe的点击
			$('.iframe_div').click(function(e) {
				if ($(e.currentTarget).hasClass('cur_edit_con')) {
					return
				}
				// 删除占位元素
				$('._holder').remove()
				$('.edit_edit_btn').hide()
				$('.art_section_edit').removeClass('hidden')
				$('.art-section').css('margin-bottom', '30px')
				$('.cur_edit_con')
					.closest('.art-section')
					.removeClass('padding_none')
				$('.cur_edit_con').removeClass('cur_edit_con')
				$('.art-content')
					.find('.cur_art_section')
					.removeClass('cur_art_section')
				$(this)
					.parent()
					.addClass('cur_edit_con')
				$('.cur_edit_con')
					.closest('.art-section')
					.addClass('padding_none')
				$(this)
					.parent()
					.after($('.art_section_edit'))
				$('.art_section_edit').css('margin-bottom', '30px')
				$(this)
					.parent()
					.css('margin-bottom', '0')
				$('.art_section_edit').css('margin-bottom', '30px')
				scrollToEl()
			})
			// 新的文章编辑的iframe处理
			$('._iframe_editor').click(function(e) {
				if ($(e.currentTarget).hasClass('cur_edit_con')) {
					return
				}
				// 删除占位元素
				$('._holder').remove()
				$('.edit_edit_btn').hide()
				$('.art_section_edit').removeClass('hidden')
				$('.cur_edit_con').removeClass('cur_edit_con')
				$('.art-content')
					.find('.cur_art_section')
					.removeClass('cur_art_section')
				$(this)
					.parent()
					.addClass('cur_edit_con')
				$(this)
					.parent()
					.after($('.art_section_edit'))
				scrollToEl()
			})
			// 头部添加内容
			$('.edit_add_wrap').on('click', function(e) {
				if ($(e.currentTarget).hasClass('cur_edit_con')) {
					return
				}
				// 删除占位元素
				$('._holder').remove()
				$('.art-section').css('margin-bottom', '30px')
				$('.edit_add_con_wrap').hasClass('hidden')
					? $('.edit_add_con_wrap').removeClass('hidden')
					: $('.edit_add_con_wrap').addClass('hidden')
				$('.cur_edit_con')
					.closest('.art-section')
					.removeClass('padding_none')
				$('.cur_edit_con').removeClass('cur_edit_con')
				$('.art_section_edit').addClass('hidden')
			})
			$(document).click(function(e) {
				if (
					$(e.target).closest('.edit_add_wrap').length > 0 ||
					$(e.target).closest('.edit_add_con_wrap').length > 0
				) {
					return
				}
				$('.edit_add_con_wrap').addClass('hidden')
			})
			// 顶部添加文本
			$('.edit_text_cancel').on('click', function() {
				isAddTop = false
				$('#summernote').summernote('code', '')
				$.closePopup()
				stopBodyScroll(false)
			})
			$('.edit_text_confirm').on('click', function() {
				var topStr = $('#summernote').summernote('code')
				// _holder为占位元素
				var _html =
					'<div class="_holder" style="height: 52px;"></div><p class="art-section-new">' +
					topStr +
					'</p>'
				if ($('#summernote').summernote('isEmpty') && editTextStatus != 5) {
					$.toast('请输入文字', 'text')
					return
				}
				if (editTextStatus == 1) {
					// 顶部添加文本
					console.log('顶部文字')
					$('.art-content').prepend(_html)
					$('._holder').remove()
				} else if (editTextStatus == 2) {
					// 添加文本
					if ($('.cur_edit_con').closest('._135editor').length > 0) {
						$('.art_section_edit').after(_html)
						$('#summernote').summernote('code', '')
						$.closePopup()
						return
					}
					if ($('.cur_edit_con').closest('.art-section').length) {
						// 旧版之前文章的div
						$('.cur_edit_con')
							.closest('.art-section')
							.addClass('cur_art_section')
						$('.cur_art_section')
							.next()
							.hasClass('art_section_edit')
							? $('.art_section_edit').after(_html)
							: $('.cur_art_section').after(_html)
					} else {
						$('.art_section_edit').after(_html)
					}
					// else if ($('.cur_edit_con').closest('.art-section-new').length) {
					//   // 新版新加的段落，图片，产品都会是art-section-new的类
					//   $('.cur_edit_con').closest('.art-section-new').addClass('cur_art_section');
					//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
					// } else if ($('.cur_edit_con').closest('._135editor').length) {
					//   // 这个是135编辑器的类
					//   $('.cur_edit_con').closest('._135editor').addClass('cur_art_section');
					//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
					// } else if ($('.cur_edit_con').closest('.other-section').length) {
					//   // 其他文章的情况
					//   $('.cur_edit_con').closest('.other-section').addClass('cur_art_section');
					//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
					// }
				} else if (editTextStatus == 4) {
					if (topStr.length > 64) {
						$.toast('文章标题最多输入64个字', 'text')
						return
					}
					$('.article_title_wrap .article_title').text($(_html).text())
				} else if (editTextStatus == 5) {
					if (topStr.length > 120) {
						$.toast('文章摘要最多输入64个字', 'text')
						return
					}
					article_des = $('#summernote').summernote('isEmpty')
						? ''
						: $(_html).text()
					checkArticleDes()
				} else {
					// 修改
					$('.cur_edit_con').html(topStr)
				}
				// articleEventListener();
				$('#summernote').summernote('code', '')
				$.closePopup()
				$('.edit_add_con_wrap').addClass('hidden')
			})
			// 为文章内容添加监听事件
			articleEventListener()
			// 点击产品分类
			// 险种分类tab
			var insureTabStr = ''
			if (companyArr.length > 0) {
				getInsureList(curCompanyId, pageIndex)
				for (var i = 0; i < companyArr.length; i++) {
					if (i == 0) {
						insureTabStr +=
							'<div class="pro_slide_li pro_slide_active" data-company_id="' +
							companyArr[i].company_id +
							'">' +
							'<div class="pro_item_text">' +
							companyArr[i].company_name +
							'</div>' +
							'<div class="pro_item_line"></div>' +
							'</div>'
					} else {
						insureTabStr +=
							'<div class="pro_slide_li" data-company_id="' +
							companyArr[i].company_id +
							'">' +
							'<div class="pro_item_text">' +
							companyArr[i].company_name +
							'</div>' +
							'<div class="pro_item_line"></div>' +
							'</div>'
					}
				}
				$('.pro_slide_ul').append(insureTabStr)
			} else {
				if ($('.pro_content_inner').html() != '') {
					$('.add_pro_btn').removeClass('hidden')
				} else {
					$('.add_pro_btn').addClass('hidden')
				}
			}
			$('.pro_slide_ul .pro_slide_li').on('click', function() {
				$('.pro_slide_ul .pro_slide_active').removeClass('pro_slide_active')
				$(this).addClass('pro_slide_active')
			})
			// 产品列表滚动加载
			$('.pro_wrapper').infinite()
			// 监听产品滚动到底部  加载更多
			$('.pro_wrapper')
				.infinite()
				.on('infinite', function() {
					// if ($('.pro_wrapper .weui-loadmore').css('dispaly') == 'block') return
					if (loading) return
					loading = true
					if ($('.no_more').css('display') == 'none') {
						pageIndex += 1
						// 加载更多
						getInsureList(curCompanyId, pageIndex)
					}
				})
			// 监听弹框关闭
			$('#pro_wrap').on('click', function(e) {
				stopBodyScroll(false)
			})
			// 选择公司 产品
			$('.pro_slide_ul .pro_slide_li').on('click', function(e) {
				curCompanyId = $(this).data('company_id')
				$('.pro_slide_ul .pro_slide_li').removeClass('pro_slide_active')
				$(this).addClass('pro_slide_active')
				pageIndex = 0
				$('.pro_content_inner').empty()
				$('.no_more').hide()
				// 获取产品列表
				getInsureList(curCompanyId, pageIndex)
			})
			// 旧版插入的产品 图片  文本  添加点击事件
			$('.art-content').on(
				'click',
				'.product-section, .art-section-img, .art-section-text',
				function(e) {
					if (
						$(e.currentTarget).hasClass('product-section') ||
						$(e.currentTarget).hasClass('art-section-img')
					) {
						$('.edit_edit_btn').hide()
					} else {
						$('.edit_edit_btn').show()
					}
					$('.art_section_edit').removeClass('hidden')
					$('.art-section').css('margin-bottom', '30px')
					$('.cur_edit_con')
						.closest('.art-section')
						.removeClass('padding_none')
					$('.cur_edit_con').removeClass('cur_edit_con')
					$('.art-content')
						.find('.cur_art_section')
						.removeClass('cur_art_section')
					$(this).addClass('cur_edit_con')
					$('.cur_edit_con')
						.closest('.art-section')
						.addClass('padding_none')
					$(this).after($('.art_section_edit'))
					$('.art_section_edit').css('margin-bottom', '30px')
					$(this).css('margin-bottom', '0')
					$('.art_section_edit').css('margin-bottom', '30px')
					scrollToEl()
				}
			)
			// 新版插入的div为 art-section-new
			$('.art-content').on('click', '.art-section-new', function(e) {
				// 删除占位元素
				$('._holder').remove()
				if ($(e.currentTarget).hasClass('product-section')) {
					$(this).removeAttr('style')
					return
				}
				$('.art_section_edit').removeClass('hidden')
				$('.cur_edit_con').removeClass('cur_edit_con')
				$('.art-content')
					.find('.cur_art_section')
					.removeClass('cur_art_section')
				$(this).addClass('cur_edit_con')
				$(this).after($('.art_section_edit'))
			})

			// 修改文章标题
			$('.article_title_wrap .article_title').click(function() {
				editTextStatus = 4
				var curContent = $('.article_title_wrap .article_title').text()
				$('#summernote').summernote('code', curContent)
				$('#edit_text').popup()
			})
			// 修改文章摘要
			$('.article_title_other .article_title_des').click(function() {
				editTextStatus = 5
				var curContent = $('.article_title_other .article_title_des').text()
				$('#summernote').summernote('code', curContent)
				$('#edit_text').popup()
			})
			// 修改文章封面
			$('.article_title_wrap .article_cover_img').click(function() {
				wx.chooseImage({
					count: 1,
					sizeType: ['compressed'], //压缩图
					success: function(res) {
						if (!res.localIds) {
							return
						}
						var localIds = res.localIds.toString()
						$('.inner_cover_img').attr('src', localIds)
						function uploadAvatar() {
							wx.uploadImage({
								localId: localIds,
								isShowProgressTips: 1, // 默认为1，显示进度提示
								success: function(res) {
									$.toast('上传成功', 'text')
									article_cover_media_id = res.serverId
								},
								fail: function(res) {
									$.toast('上传失败', 'text')
								}
							})
						}
						uploadAvatar()
					}
				})
			})
			// 保存文章
			$('#save_article').click(function() {
				var article_id = '7wPjLi7QwcwUF'
				$.showLoading('保存中...')
				var art_title = $('.article_title_wrap .article_title').text()
				var article_sub_title = $('.article_title_wrap .article_title_des').text()
				if ($('.art-content .cur_edit_con').hasClass('art-section')) {
					$('.art-content .cur_edit_con').css('margin-bottom', '30px')
				}
				$('.art-content .cur_edit_con').removeClass('cur_edit_con')
				// 还原art_section_edit
				$('.art_section_edit_wrap').html($('.art_section_edit'))
				$('.art-content .padding_none').removeClass('padding_none')
				$('.art-content .cur_art_section').removeClass('.cur_art_section')
				$('.art-content .consult-column').removeClass('hidden')
				// 处理iframe的元素删除
				$('.art-content .iframe_div').remove()
				if (revoke_arr.length > 0) {
					for (var m = 0; m < revoke_arr.length; m++) {
						$('.' + revoke_arr[m]).remove()
					}
				}
				var page_html = $('.art-content').html()
				$.ajax({
					url: '/index.php/Index/tthk/saveArticle',
					type: 'post',
					data: {
						article_id: article_id,
						content: page_html,
						uid: uid,
						title: art_title,
						article_sub_title: article_sub_title,
						article_cover_media_id: article_cover_media_id
					},
					dataType: 'json',
					success: function(res) {
						$.hideLoading()
						if (res.code == 0) {
							var art_id = res.id
							$.toast('保存成功', 'text')
							window.location.href =
								'/index.php/Index/tthk/article_content/article_id/' +
								art_id +
								'/uid/' +
								uid +
								'/edit/0/ad/1'
						} else {
							if (res.data) {
								if (res.data.feedback) {
									var feedBackImgArr = res.data.feedback
									var _htmlStr = ''
									for (var i = 0; i < feedBackImgArr.length; i++) {
										_htmlStr +=
											'<div class="feed_item" data-scenes="' +
											feedBackImgArr[i].scenes +
											'" data-type="' +
											feedBackImgArr[i].type +
											'" data-location="' +
											feedBackImgArr[i].location +
											'" data-url="' +
											feedBackImgArr[i].url +
											'">' +
											'<div class="select_icon hidden">' +
											'<img src="https://staticoss.bxdaka.com/static/images/feed_select.png" alt="">' +
											'</div>' +
											'<img class="ban_icon hidden" src="https://staticoss.bxdaka.com/static/images/ban_icon.png" alt="">' +
											'<div class="feed_item_img_w">' +
											'<img class="feed_item_img" src="' +
											feedBackImgArr[i].url +
											'" alt = "" >' +
											'<div class="filter_modal hidden"></div>' +
											'</div>' +
											'<div class="feed_item_txt">' +
											feedBackImgArr[i].text +
											'</div>' +
											'</div>'
									}
									// 重置状态
									$('.feed_footer .feed_btn').removeClass('hidden')
									$('.feed_footer .feed_cancel').addClass('hidden')
									$('.feed_footer .back_edit').removeClass('hidden')
									$('.feed_footer .feed_submit').addClass('hidden')
									$('.feed_con .feed_item').removeClass(
										'feed_item_active'
									)
									$('.feed_con').empty()
									$('.feed_con').append(_htmlStr)
									$('.feed_con .feed_item').on('click', function() {
										var curType = $(this).data('type')
										if (
											curType == 'porn' ||
											curType == 'terrorism' ||
											curType == 'ad'
										) {
											if (
												$('.feed_footer_l .feed_btn').hasClass(
													'hidden'
												)
											) {
												$(this).hasClass('feed_item_active')
													? $(this).removeClass(
															'feed_item_active'
													  )
													: $(this).addClass('feed_item_active')
											}
										}
									})
									$('#feed_popup').popup()
								} else {
									$.toast(res.msg, 'text')
								}
							} else {
								$.toast(res.msg, 'text')
							}
						}
					},
					error: function(res) {
						$.toast('保存失败，请重试')
					}
				})
			})
			// 识别有误反馈
			$('.feed_footer .feed_btn').on('click', function() {
				$('.feed_footer .feed_btn').addClass('hidden')
				$('.feed_footer .feed_cancel').removeClass('hidden')
				$('.feed_footer .back_edit').addClass('hidden')
				$('.feed_footer .feed_submit').removeClass('hidden')
				$('.feed_con .feed_item').each(function() {
					var curType = $(this).data('type')
					if (curType == 'porn' || curType == 'terrorism' || curType == 'ad') {
						$(this)
							.find('.ban_icon')
							.addClass('hidden')
						$(this)
							.find('.filter_modal')
							.addClass('hidden')
						$(this)
							.find('.select_icon')
							.removeClass('hidden')
					} else {
						$(this)
							.find('.select_icon')
							.addClass('hidden')
						$(this)
							.find('.ban_icon')
							.removeClass('hidden')
						$(this)
							.find('.filter_modal')
							.removeClass('hidden')
					}
				})
			})
			$('.feed_footer .feed_cancel').on('click', function() {
				$('.feed_footer .feed_btn').removeClass('hidden')
				$('.feed_footer .feed_cancel').addClass('hidden')
				$('.feed_footer .back_edit').removeClass('hidden')
				$('.feed_footer .feed_submit').addClass('hidden')
				$('.feed_con .feed_item .select_icon').removeClass('select_icon_active')
				$('.feed_con .feed_item .select_icon').addClass('hidden')
				$('.feed_con .feed_item .ban_icon').addClass('hidden')
				$('.feed_con .feed_item .filter_modal').addClass('hidden')
			})
			$('.back_edit').click(function() {
				$('.feed_con').empty()
				$.closePopup()
			})
			$('.feed_submit').click(function() {
				var feedImgArr = []
				if ($('.feed_con .feed_item_active').length <= 0) {
					$.toast('无反馈内容', 'text')
					return
				}
				$('.feed_con .feed_item_active').each(function() {
					var feedImgItem = {}
					feedImgItem.url = $(this).data('url')
					feedImgItem.location = $(this).data('location')
					feedImgItem.type = $(this).data('type')
					feedImgItem.scene = $(this).data('scenes')
					feedImgArr.push(feedImgItem)
				})
				$.ajax({
					url: '/index/feedback/send',
					type: 'post',
					data: {
						uid: uid,
						from: 0,
						value: '7wPjLi7QwcwUF',
						appid: appId,
						strurl: JSON.stringify(feedImgArr)
					},
					dataType: 'json',
					success: function(res) {
						console.log(res)
						if (res.code == 0) {
							$.toast('反馈成功', 'text')
							$('.feed_con').empty()
							$.closePopup()
						} else {
							$.toast(res.msg, 'text')
						}
					},
					fail: function(res) {
						alert('请求失败')
					}
				})
			})
		})

		// 监听页面返回
		// function pushHistory() {
		//   let state = {
		//     title: article_title,
		//     url: window.location.href
		//   };
		//   window.history.pushState(state, state.title, state.url);
		// }
		// function windowListener() {
		//   $.modal({
		//     title: "",
		//     text: "您正在编辑中,退出关闭前请先存为草稿",
		//     buttons: [
		//       {
		//         text: "直接退出", onClick: function () {
		//           window.history.back();
		//         }
		//       },
		//       { text: "取消", className: 'default', onClick: function () { pushHistory() } },
		//     ]
		//   });
		// }
		;(function() {
			function lazy() {
				var s = document.createElement('script')
				s.type = 'text/javascript'
				s.src = 'https://s23.cnzz.com/z_stat.php?id=1277638470&web_id=1277638470'
				document.body.appendChild(s)
			}
			window.addEventListener('load', lazy, false)
		})()
	},
	methods: {
		//获取上传图片
		afterRead1(file) {
			this.imgUrl = file.content
		},
		afterRead2(file) {
			console.log(2, file.content)
			var _html = ''
			_html +=
				'<div class="art-section-new"><img src="' + file.content + '"/></div>'
			$('.art-content').prepend(_html)
			articleEventListener()
			$.toast('上传成功', 'text')
		},
		afterRead3(file) {
			var _html = ''
			_html +=
				'<div class="art-section-new"><img src="' + file.content + '"/></div>'
			if ($('.cur_edit_con').closest('.art-section').length) {
				// 旧版之前文章的div
				$('.cur_edit_con')
					.closest('.art-section')
					.addClass('cur_art_section')
				$('.cur_art_section')
					.next()
					.hasClass('art_section_edit')
					? $('.art_section_edit').after(_html)
					: $('.cur_art_section').after(_html)
			} else {
				$('.art_section_edit').after(_html)
			}

			articleEventListener()
		},
		//删除
		deleteEl() {
			del_num += 1
			revoke_arr.push('revoke_' + del_num)
			$('.cur_edit_con').addClass('hidden revoke_' + del_num)
			$('.cur_edit_con')
				.closest('.art-section')
				.removeClass('padding_none')
			$('.cur_edit_con').removeClass('cur_edit_con')
			$('.art_section_edit').addClass('hidden')
		},
		//修改
		editEdit() {
			editTextStatus = 3
			var curContent = $('.cur_edit_con').html()
			$('#summernote').summernote('code', curContent)
			$('#edit_text').popup()
		},
		// 加文字
		editAddText() {
			console.log('添加文字')
			editTextStatus = 2
			$('#edit_text').popup()
		},
		// 顶部加文字
		editAddTopText() {
			console.log('顶部添加文字')
			editTextStatus = 1
			$('#edit_text').popup()
		},
		// 加图片
		editAddImg() {
			console.log('图加图')
			wx.chooseImage({
				count: 1,
				sizeType: ['compressed'],
				success: function(res) {
					if (!res.localIds) {
						return
					}
					var localIds = res.localIds.toString()
					// alert(localIds)
					uploadImg(localIds)
				}
			})
			function uploadImg(ids) {
				wx.uploadImage({
					localId: ids,
					success: function(res) {
						$.ajax({
							type: 'POST',
							url: '/index.php/index/tthk/uploadQiniu',
							data: { article_pic: res.serverId },
							dataType: 'json',
							success: function(res) {
								// alert(res.url)
								var _html = ''
								_html +=
									'<div class="art-section-new"><img src="' +
									res.url +
									'"/></div>'
								if (isAddTop) {
									$('.art-content').prepend(_html)
								} else {
									if (
										$('.cur_edit_con').closest('.art-section').length
									) {
										// 旧版之前文章的div
										$('.cur_edit_con')
											.closest('.art-section')
											.addClass('cur_art_section')
										$('.cur_art_section')
											.next()
											.hasClass('art_section_edit')
											? $('.art_section_edit').after(_html)
											: $('.cur_art_section').after(_html)
									} else {
										$('.art_section_edit').after(_html)
									}
									// else if ($('.cur_edit_con').closest('.art-section-new').length) {
									//   // 新版新加的段落，图片，产品都会是art-section-new的类
									//   $('.cur_edit_con').closest('.art-section-new').addClass('cur_art_section');
									//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
									// } else if ($('.cur_edit_con').closest('._135editor').length) {
									//   // 这个是135编辑器的类
									//   $('.art_section_edit').after(_html)
									// } else if ($('.cur_edit_con').closest('.other-section').length) {
									//   // 其他文章的情况
									//   $('.cur_edit_con').closest('.other-section').addClass('cur_art_section');
									//   $('.cur_art_section').next().hasClass('art_section_edit') ? $('.art_section_edit').after(_html) : $('.cur_art_section').after(_html);
									// }
								}
								// 重置
								isAddTop = false
								// articleEventListener();
								$.toast('上传成功', 'text')
							}
						})
					}
				})
			}
		},
		// 关闭产品弹框
		closeProModal() {
			$.closePopup()
			// 释放body滚动
			stopBodyScroll(false)
			// 禁止body滚动
			function stopBodyScroll(isFixed) {
				if (isFixed) {
					$('body, html').css({
						overflow: 'hidden'
					})
				} else {
					$('body, html').css({
						overflow: 'auto'
					})
				}
			}
		},
		// 顶部加图片
		addTopImg() {
			isAddTop = true
			editAddImg()
		},
		// 撤销删除
		cancelDelete() {
			var revoke_len = revoke_arr.length
			if (revoke_arr.length == 0) {
				$.toast('无撤销内容', 'text')
				return
			}
			revoke_arr.pop()
			del_num = revoke_len - 1
			if ($('.revoke_' + revoke_len).hasClass('art-section')) {
				$('.revoke_' + revoke_len).css('margin-bottom', '30px')
			}
			$('.revoke_' + revoke_len).removeClass('hidden revoke_' + revoke_len)
			// $.toast('撤销成功', 'text');
		}
	}
}
</script>

<style type="text/css">
::-webkit-scrollbar {
	width: 12px !important;
	height: 12px !important;
}
::-webkit-scrollbar-thumb:vertical {
	background-color: rgba(136, 141, 152, 0.5) !important;
	border-radius: 10px !important;
	background-clip: content-box !important;
	border: 2px solid transparent !important;
}
::-webkit-scrollbar-thumb:horizontal {
	background-color: rgba(136, 141, 152, 0.5) !important;
	border-radius: 10px !important;
	background-clip: content-box !important;
	border: 2px solid transparent !important;
}
::-webkit-resizer {
	display: none !important;
}
::-webkit-scrollbar {
	/*隐藏滚轮*/
	display: none;
}

.hidden {
	display: none !important;
}

body {
	background: #fff;
}

h1,
h2,
h3,
h4,
h5,
h6 {
	font-size: 19px;
}

li {
	list-style: none;
}

a {
	font-size: 14px;
	color: #333;
	text-decoration: none;
}

a:active {
	text-decoration: none;
}

article,
section {
	max-width: 100% !important;
	box-sizing: border-box;
}

pre {
	white-space: pre-wrap;
	/* css-3 */
	white-space: -moz-pre-wrap;
	/* Mozilla, since 1999 */
	white-space: -pre-wrap;
	/* Opera 4-6 */
	white-space: -o-pre-wrap;
	/* Opera 7 */
	word-wrap: break-word;
	/* Internet Explorer 5.5+ */
}

.container,
textarea,
input {
	color: #333;
	font-family: 'PingFangSC-Regular', '微软雅黑', 'Microsoft Yahei', 'Avenir', Helvetica,
		Arial, sans-serif;
	font-size: 17px;
	padding-bottom: 25px;
	background: #f6f6f6;
}

.clear:after,
.product-info:after,
.consult-column:after {
	clear: both;
	content: '.';
	display: block;
	height: 0;
	overflow: hidden;
	visibility: hidden;
}

.fixed_center {
	position: fixed;
	top: 50%;
	left: 50%;
	-webkit-transform: translate(-50%, -50%);
	-ms-transform: translate(-50%, -50%);
	transform: translate(-50%, -50%);
}

img {
	max-width: 100% !important;
	height: auto !important;
	margin: 0 auto;
}

/*编辑文章提示*/
.edit_notice_wrap {
	position: fixed;
	width: 100%;
	height: 100%;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-orient: vertical;
	-webkit-box-direction: normal;
	-ms-flex-direction: column;
	flex-direction: column;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	top: 0;
	left: 0;
	background: rgba(0, 0, 0, 0.6);
	color: #fff;
	text-align: center;
	z-index: 1000;
}

.edit_notice_wrap .edit_notice_title {
	font-size: 36px;
	font-weight: bold;
	text-align: center;
	margin-top: 12.8%;
	line-height: 50px;
}

.edit_notice_wrap .edit_notice_y {
	color: #fdc50a;
}

.edit_notice_wrap .edit_notice_img {
	width: 240px;
	margin-top: 5%;
}

.edit_notice_wrap .notice_btn {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	height: 50px;
	margin-top: 5.5%;
}

.notice_btn .notice_btn_item {
	width: 140px;
	height: 50px;
	border-radius: 4px;
	line-height: 50px;
	text-align: center;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}

.notice_btn .no_notice {
	border: 1px solid rgba(255, 255, 255, 1);
}

.notice_btn .notice_known {
	background: #e02e42;
	margin-left: 15px;
}

/*文章标题, 背景图*/
.article_title_wrap {
	width: 100%;
	padding: 15px;
	background: #fff;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}

.article_title_wrap .article_title {
	font-weight: bold;
	line-height: 24px;
	margin-bottom: 18px;
}

.article_title_wrap .article_title_other {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
}

.article_title_wrap .article_title_des {
	font-size: 14px;
	color: #999999;
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	line-height: 22px;
	margin-right: 10px;
}

.article_title_wrap .article_cover_img {
	position: relative;
	width: 80px;
	height: 80px;
}

.article_cover_img .inner_cover_img {
	width: 100%;
	height: 100% !important;
}

.article_cover_img .opacity_cover {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: rgba(0, 0, 0, 0.3);
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-orient: vertical;
	-webkit-box-direction: normal;
	-ms-flex-direction: column;
	flex-direction: column;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	font-size: 14px;
	color: #fff;
}

.opacity_cover .opacity_cover_img {
	width: 24px;
	margin-bottom: 5px;
}

/*文章摘要*/
.article_des_wrap .article_des_title {
	font-size: 14px;
	padding-left: 15px;
	line-height: 45px;
}

.article_des_wrap .article_des_con {
	padding: 10px 15px;
	background: #fff;
}

.article_des_con .no_des {
	font-size: 17px;
	line-height: 50px;
	color: #b6b6b6;
}

/*文章内容*/
.art-content {
	padding: 0 15px 30px;
	max-width: 100%;
	overflow: hidden;
}

.art-content .art-section {
	margin-bottom: 30px;
	padding: 0 15px;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
	line-height: 34px;
}

.art-content .padding_none {
	padding-bottom: 0;
}

.art-content .art-section:nth-last-child(1) {
	margin-bottom: 0;
}

/* .art-content .art-section p {
		padding-bottom: 5px;
	  } */

/*产品*/
.art-content .product-section {
	background: #ffffff;
	padding: 15px !important;
}

.product-section .product-info img {
	width: 72px;
	height: 72px;
	float: left;
}

.product-section .product-info h3 {
	white-space: nowrap;
	font-size: 17px;
	font-weight: bold;
	margin-left: 87px;
	text-align: left;
	overflow: hidden;
	line-height: 24px;
	-o-text-overflow: ellipsis;
	text-overflow: ellipsis;
}

.product-section .product-info .cont {
	font-size: 14px;
	line-height: 21px;
	text-align: left;
	color: #999999;
	margin: 6px 0 0 87px;
	overflow: hidden;
	-o-text-overflow: ellipsis;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}

.product-section .consult-column {
	/* padding-bottom: 15px; */
	margin-top: 25px;
}

.product-section .consult-column img {
	width: 32px;
	height: 32px;
	border-radius: 50%;
	font-size: 14px;
	float: left;
}

.product-section .consult-column i {
	line-height: 32px;
	font-style: normal;
	margin-left: 10px;
	float: left;
}

.product-section .consult-column span {
	padding: 6px 12px;
	background: #e02e42;
	border-radius: 2px;
	color: #fff;
	text-align: center;
	line-height: 20px;
	float: right;
}

.product-section .hr,
.product-section .scale-half {
	border: none;
}

/*编辑*/
.edit_top {
	position: relative;
	height: 60px;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
}

.edit_top .edit_add_wrap {
	width: 30px;
	height: 30px;
}

.edit_top .edit_add_con_wrap {
	position: absolute;
	top: 56px;
	left: 50%;
	-webkit-transform: translateX(-50%);
	-ms-transform: translateX(-50%);
	transform: translateX(-50%);
	z-index: 8;
}

.edit_top .edit_add_con_wrap::before {
	content: '';
	width: 0px;
	height: 0px;
	border-left: 5px solid transparent;
	border-right: 5px solid transparent;
	border-bottom: 5px solid #fff;
	position: absolute;
	top: -5px;
	left: 50%;
	-webkit-transform: translateX(-50%);
	-ms-transform: translateX(-50%);
	transform: translateX(-50%);
}

.edit_top .edit_add_con {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	padding: 12px 14px;
	border-radius: 5px;
	background: #fff;
	line-height: 22px;
}

.edit_add_con .edit_btn_item_t {
	display: -webkit-box;
	display: -ms-flexbox;
	width: 62px;
	display: flex;
	-webkit-box-orient: vertical;
	-webkit-box-direction: normal;
	-ms-flex-direction: column;
	flex-direction: column;
	font-size: 16px;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
}

.art_section_edit .edit_btn_item_t {
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-orient: vertical;
	-webkit-box-direction: normal;
	-ms-flex-direction: column;
	flex-direction: column;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	font-size: 16px;
}

.edit_add_con .edit_btn_item_t:nth-last-child(1) {
	margin-right: 0;
}

.edit_btn_item_t .edit_btn_txt_icon_t {
	width: 36px;
	height: 36px;
	background-image: url(https://staticoss.bxdaka.com/static/images/edit_txt.png);
	background-size: cover;
	background-repeat: no-repeat;
}

.edit_btn_item_t .edit_btn_img_icon_t {
	width: 36px;
	height: 36px;
	background-image: url(https://staticoss.bxdaka.com/static/images/edit_img.png);
	background-size: cover;
	background-repeat: no-repeat;
}

.edit_btn_item_t .edit_btn_pro_icon_t {
	width: 36px;
	height: 36px;
	background-image: url(https://staticoss.bxdaka.com/static/images/edit_pro.png);
	background-size: cover;
	background-repeat: no-repeat;
}

.edit_btn_item_t .edit_btn_txt_t {
	margin-top: 5px;
	font-weight: normal;
	color: #333;
	font-size: 16px;
}

.art_section_edit .edit_btn_item {
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	font-size: 16px;
}

.edit_btn_item .edit_btn_delete_icon {
	width: 17px;
	height: 17px;
	background-image: url(https://staticoss.bxdaka.com/static/images/c_delete_icon.png);
	background-size: cover;
	background-repeat: no-repeat;
	margin: 4px 3px 0 0;
}

.edit_btn_item .edit_btn_edit_icon {
	width: 17px;
	height: 17px;
	background-image: url(https://staticoss.bxdaka.com/static/images/c_edit_icon.png);
	background-size: cover;
	background-repeat: no-repeat;
	margin: 4px 3px 0 0;
}

.edit_btn_item .edit_btn_txt_icon,
.edit_btn_item .edit_btn_img_icon,
.edit_btn_item .edit_btn_pro_icon,
.edit_btn_item .edit_btn_house_icon {
	width: 17px;
	height: 17px;
	background-image: url(https://staticoss.bxdaka.com/static/images/c_add_icon.png);
	background-size: cover;
	background-repeat: no-repeat;
	margin: 4px 3px 0 0;
}

.edit_btn_item .edit_btn_txt {
	margin-top: 5px;
	font-weight: normal;
	color: #333;
	font-size: 16px;
	font-style: normal;
}

/*编辑文本弹出层*/
textarea {
	display: block;
	width: 92%;
	outline: none;
	resize: none;
	border: none;
	font-size: 17px;
	margin: 15px auto;
	padding: 8px 15px;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}

#edit_text .edit_text_btn {
	width: 92%;
	margin: 20px auto;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-pack: justify;
	-ms-flex-pack: justify;
	justify-content: space-between;
}

.edit_text_btn .edit_text_cancel,
.edit_text_btn .edit_text_confirm {
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	height: 50px;
	text-align: center;
	border-radius: 4px;
	font-size: 16px;
	line-height: 50px;
}

.edit_text_btn .edit_text_cancel {
	background: #e2e2e2;
}

.edit_text_btn .edit_text_confirm {
	background: #e02e42;
	margin-left: 20px;
	color: #fff;
}

.art-content .cur_edit_con {
	display: block;
	width: 100%;
	margin-left: 0 !important;
	margin-right: 0 !important;
	margin-bottom: 0 !important;
	background: #ffeeef !important;
	border: 1px dashed #e02e42 !important;
	padding: 10px 15px;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
	box-shadow: 0px 2px 5px #999;
	float: none !important;
}

/*编辑按钮框*/
.art_section_edit {
	position: absolute;
	left: 15px;
	right: 15px;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-ms-flex-pack: distribute;
	justify-content: space-around;
	height: 52px;
	background: #fff;
	margin-bottom: 20px;
	box-shadow: 0px 2px 5px #999;
	z-index: 8;
}

.footer,
.footer_bar {
	height: 54px;
}

.footer {
	width: 100%;
	position: fixed;
	bottom: 0;
	left: 0;
	z-index: 9;
}

.footer {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
}

.footer .footer_l,
.footer .footer_r {
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	text-align: center;
	line-height: 54px;
	font-size: 16px;
}

.footer .footer_l {
	background: #eee;
}

.footer .footer_r {
	background: #e02e42;
	color: #fff;
}

/*隐藏audio， video下载按钮*/
video::-webkit-media-controls-enclosure {
	overflow: hidden;
}

video::-webkit-media-controls-panel {
	width: calc(100% + 30px);
}

audio::-internal-media-controls-download-button {
	display: none;
}

audio::-webkit-media-controls-enclosure {
	overflow: hidden;
}

audio::-webkit-media-controls-panel {
	width: calc(100% + 30px);
}

video,
audio,
iframe {
	width: 100% !important;
}

/*weui默认主题颜色*/
.weui-dialog .weui-dialog__bd {
	color: #333;
}

.weui-dialog .weui-dialog__btn {
	color: #e02e42;
}

.weui-dialog .continue_edit {
	color: #333;
}

.weui-dialog .free_edit_num {
	color: #db273d;
}

.edit_article {
	position: fixed;
	bottom: 50px;
	right: 15px;
	width: 90px;
	height: 86px;
	z-index: 1;
}

.art-section strong,
.art-section b {
	color: #e02e42;
}

.note-popover .popover-content,
.panel-heading.note-toolbar {
	display: none !important;
}

/*选择产品*/
.pro_content {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-orient: vertical;
	-webkit-box-direction: normal;
	-ms-flex-direction: column;
	flex-direction: column;
	max-height: 485px;
	background: #fff;
	border-radius: 16px 16px 0 0;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}

.pro_content .pro_slide_bar {
	width: 100%;
	height: 58px;
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
}

.pro_slide_bar .pro_slide_ul {
	white-space: nowrap;
	padding: 0 13px;
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	overflow: auto;
	-webkit-overflow-scrolling: touch;
}

.pro_slide_ul .pro_slide_li {
	display: inline-block;
	line-height: 55px;
	font-size: 16px;
	margin: 0 7px;
}

.pro_slide_li .pro_item_line {
	width: 15px;
	height: 3px;
	background: #fff;
	margin: 0 auto;
}

.pro_slide_ul .pro_slide_active {
	color: #e02e42;
}

.pro_slide_active .pro_item_line {
	background: #e02e42;
}

.pro_slide_bar .close_con {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	-webkit-box-align: center;
	-ms-flex-align: center;
	align-items: center;
	-webkit-box-pack: center;
	-ms-flex-pack: center;
	justify-content: center;
	width: 58px;
	height: 58px;
}

.close_con img {
	width: 18px;
	height: 18px;
}

.pro_content .pro_wrapper {
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	overflow: auto;
	-webkit-overflow-scrolling: touch;
}

.pro_content .pro_list_con {
	margin: 0 15px 10px;
	background: #f7f7f7;
	padding: 15px;
}

.pro_list_con img {
	width: 72px;
	height: 72px;
	float: left;
}

.pro_list_con .pro_list_info {
	margin-left: 87px;
}

.pro_list_con .pro_list_title {
	font-size: 17px;
	line-height: 24px;
	font-weight: bold;
}

.pro_list_con .pro_list_des {
	font-size: 15px;
	color: #999999;
	line-height: 21px;
	margin-top: 6px;
}

.weui-loadmore {
	display: none;
}

.no_more {
	line-height: 30px;
	font-size: 13px;
	color: #999;
	text-align: center;
	display: none;
}

.edit_btn_item:active {
	background: #f3f3f3;
}

.footer_l:active {
	background: #ccc;
}

.notice_known:active,
#save_article:active {
	background: #be2738;
}

@media screen and (max-width: 374px) {
	.edit_notice_wrap .edit_notice_img {
		width: 200px;
	}
}

/*135编辑器*/
._135editor {
	padding: 0 15px;
}

.art-section-new {
	margin: 15px 0;
	padding: 0 15px;
}

.content {
	padding: none;
}

/*反馈图片底部弹框*/
.feed_container {
	display: flex;
	flex-direction: column;
	width: 100%;
	max-height: 85%;
	background: #fff;
	border-radius: 16px 16px 0 0;
	color: #333;
}

.feed_container .feed_title {
	height: 44px;
	font-size: 16px;
	line-height: 44px;
	text-align: center;
	border-bottom: 1px solid #e5e5e5;
	color: #323232;
	box-sizing: border-box;
}

.feed_container .feed_con {
	width: 100%;
	flex: 1;
	padding: 4% 0 0 4%;
	font-size: 15px;
	overflow: scroll;
}

.feed_con .feed_item {
	position: relative;
	width: 44%;
	margin-right: 4%;
	text-align: center;
	float: left;
}

.feed_con .feed_item:nth-child(2n) {
	margin-right: 0;
}

.feed_item .feed_item_img_w {
	position: relative;
	width: 100%;
	height: 0;
	padding-bottom: 100%;
}

.feed_item .feed_item_img {
	position: absolute;
	width: 100%;
	height: 100% !important;
	left: 0;
}

.feed_item .filter_modal {
	position: absolute;
	width: 100%;
	height: 100%;
	left: 0;
	background: rgba(0, 0, 0, 0.6);
	z-index: 1;
}

.feed_footer {
	display: -webkit-box;
	display: -ms-flexbox;
	display: flex;
	height: 54px;
	line-height: 54px;
}

.feed_footer .feed_footer_l,
.feed_footer .feed_footer_r {
	-webkit-box-flex: 1;
	-ms-flex: 1;
	flex: 1;
	text-align: center;
	font-size: 16px;
}

.feed_footer .feed_footer_l {
	background: #eee;
}

.feed_footer .feed_footer_r {
	background: #e02e42;
	color: #fff;
}

.feed_footer_l:active {
	background: #ccc;
}

.feed_footer_r:active {
	background: #be2738;
}

.feed_item .select_icon {
	position: absolute;
	width: 24px;
	height: 24px;
	display: flex;
	align-items: center;
	justify-content: center;
	border-radius: 50%;
	border: 1px solid #fff;
	background: rgba(0, 0, 0, 0.2);
	top: 5px;
	right: 5px;
	box-sizing: border-box;
	z-index: 2;
}

.feed_item .ban_icon {
	position: absolute;
	width: 24px;
	height: 24px;
	top: 5px;
	right: 5px;
	z-index: 2;
}

.feed_item_active .select_icon {
	background: rgba(203, 39, 61, 1);
	border: 1px solid rgba(203, 39, 61, 1);
}

.feed_item .select_icon img {
	width: 12px;
}

.feed_item .feed_item_txt {
	line-height: 21px;
	margin: 10px 0 15px 0;
}
</style>
