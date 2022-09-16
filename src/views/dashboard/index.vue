<template>
  <el-card>
    <div style="width: 100%; height: 82vh; flex-wrap: nowrap" class="dis-flex">
      <div style="width: 70%; height: 100%">
        <!-- 智能推荐 -->
        <div id="favMenu" style="width: 95%; height: 220px">
          <div style="width: 100%;height: 25px;font-size: 18px;font-weight: 700;margin-left: 12px">
            <span class="clear-title" style="position: relative;">智能推荐</span>
            <span style="font-size: 12px; color: #aaa" class="hand hand-underline" title="换一换" @click="refreshMenu">
              <i class="el-icon-refresh-right" />
            </span>
            <el-dropdown @command="handleCommand">
              <span class="el-dropdown-link">
                <i class="el-icon-arrow-down el-icon--right"></i>
              </span>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item command="3x3" :class="{'dropdown-dot':menuLayout==='3x3'}">3 X 3(推荐)</el-dropdown-item>
                <el-dropdown-item command="4x3" :class="{'dropdown-dot':menuLayout==='4x3'}">4 X 3</el-dropdown-item>
                <el-dropdown-item command="4x4" disabled>4 X 4</el-dropdown-item>
                <el-dropdown-item command="5x3" disabled>5 X 3</el-dropdown-item>
                <el-dropdown-item command="5x4" :class="{'dropdown-dot':menuLayout==='5x4'}">5 x 4</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </div>
          <div v-if="menuLayout==='3x3'" style="margin-top: 5px;height: 180px">
            <transition name="el-fade-in-linear">
              <div v-show="menuVisible" class="transition-box">
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
                  <div v-for="(item, i) in menuList0" :key="'menu0' + i" style="width: 33%; float: left">
                    <el-badge value="hot" class="menu-badge">
                      <el-button style="width: 170px" type="primary" plain :icon="i ? 'el-icon-medal' : 'el-icon-medal-1'" @click="test(item)">
                        {{ item }}
                      </el-button>
                    </el-badge>
                  </div>
                </div>
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
<!--                  <div v-for="(item, i) in menuList1" :key="'menu1' + i" style="width: 33%; float: left">-->
<!--                    <el-button type="primary" plain icon="el-icon-star-off" @click="test(item)">-->
<!--                      {{ item }}-->
<!--                    </el-button>-->
<!--                  </div>-->
                  <div style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain icon="el-icon-star-off" @click="test('交割通知单')">
                      交割通知单
                    </el-button>
                  </div>
                  <div style="width: 33%; float: left">
                    <el-button style="width: 170px;height: 33.3px" type="primary" plain @click="test('交割货款支付')">
                      <span style="position: relative;top: -5px">
                        <i style="font-size: 18px;position: relative;top: 2px" :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                        <span>交割货款支付</span>
                      </span>
                    </el-button>
                  </div>
                  <div style="width: 33%; float: left">
                    <el-popover
                      placement="right"
                      trigger="hover">
                      <span style="font-size: 12px;color: #aaa" @click="toggleHuiyuanIcon" class="hand hand-underline">{{ huiyuanicon?'点击取消收藏':'点击收藏' }}</span>
                      <el-button style="width: 170px" slot="reference" type="primary" plain :icon="{'el-icon-star-on':huiyuanicon,'el-icon-star-off':!huiyuanicon}" @click="test('会员结算业务')">
                        会员结算业务
                      </el-button>
                    </el-popover>
                  </div>
                </div>
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
                  <div v-for="(item, i) in menuList2" :key="'menu2' + i" style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain icon="el-icon-star-on" @click="test(item)">
                      <div class="text" style="max-width:140px;display: inline-block" :title="item">{{ item }}</div>
                    </el-button>
                  </div>
                </div>
              </div>
            </transition>
          </div>
          <div v-else-if="menuLayout==='4x3'" style="margin-top: 5px;height: 180px">
            <transition name="el-fade-in-linear">
              <div v-show="menuVisible" class="transition-box">
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
                  <div v-for="(item, i) in menuList0" :key="'menu0' + i" style="width: 33%; float: left">
                    <el-badge value="hot" class="menu-badge">
                      <el-button style="width: 170px" type="primary" plain :icon="i ? 'el-icon-medal' : 'el-icon-medal-1'" @click="test(item)">
                        {{ item }}
                      </el-button>
                    </el-badge>
                  </div>
                </div>
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
                  <!--                  <div v-for="(item, i) in menuList1" :key="'menu1' + i" style="width: 33%; float: left">-->
                  <!--                    <el-button type="primary" plain icon="el-icon-star-off" @click="test(item)">-->
                  <!--                      {{ item }}-->
                  <!--                    </el-button>-->
                  <!--                  </div>-->
                  <div style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain icon="el-icon-star-off" @click="test('交割通知单')">
                      交割通知单
                    </el-button>
                  </div>
                  <div style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain @click="test('交割货款支付')">
                      <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                      交割货款支付
                    </el-button>
                  </div>
                  <div style="width: 33%; float: left">
                    <el-popover
                      placement="right"
                      trigger="hover">
                      <span style="font-size: 12px;color: #aaa" @click="toggleHuiyuanIcon" class="hand hand-underline">{{ huiyuanicon?'点击取消收藏':'点击收藏' }}</span>
                      <el-button style="width: 170px" slot="reference" type="primary" plain :icon="{'el-icon-star-on':huiyuanicon,'el-icon-star-off':!huiyuanicon}" @click="test('会员结算业务')">
                        会员结算业务
                      </el-button>
                    </el-popover>
                  </div>
                </div>
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
                  <div v-for="(item, i) in menuList2" :key="'menu2' + i" style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain icon="el-icon-star-on" @click="test(item)">
                      <div class="text" style="max-width:140px;display: inline-block" :title="item">{{ item }}</div>
                    </el-button>
                  </div>
                </div>
                <div class="dis-flex" style="width: 95%;margin-bottom: 10px;">
                  <!--                  <div v-for="(item, i) in menuList1" :key="'menu1' + i" style="width: 33%; float: left">-->
                  <!--                    <el-button type="primary" plain icon="el-icon-star-off" @click="test(item)">-->
                  <!--                      {{ item }}-->
                  <!--                    </el-button>-->
                  <!--                  </div>-->
                  <div style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain icon="el-icon-star-off" @click="test('交割通知单')">
                      交割通知单
                    </el-button>
                  </div>
                  <div style="width: 33%; float: left">
                    <el-button style="width: 170px" type="primary" plain @click="test('交割货款支付')">
                      <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                      交割货款支付
                    </el-button>
                  </div>
                  <div style="width: 33%; float: left">
                    <el-popover
                      placement="right"
                      trigger="hover">
                      <span style="font-size: 12px;color: #aaa" @click="toggleHuiyuanIcon" class="hand hand-underline">{{ huiyuanicon?'点击取消收藏':'点击收藏' }}</span>
                      <el-button style="width: 170px" slot="reference" type="primary" plain :icon="{'el-icon-star-on':huiyuanicon,'el-icon-star-off':!huiyuanicon}" @click="test('会员结算业务')">
                        会员结算业务
                      </el-button>
                    </el-popover>
                  </div>
                </div>
              </div>
            </transition>
          </div>
          <div v-else-if="menuLayout==='5x4'" style="margin-top: 5px;height: 180px">
            <transition name="el-fade-in-linear">
              <div v-show="menuVisible" class="transition-box">
                <el-scrollbar style="height:175px" wrap-style="overflow-x:hidden;">
                  <div class="dis-flex" style="width: 100%;margin-bottom: 10px;">
                    <div v-for="(item, i) in menuList0" :key="'menu0' + i" style="width: 25%; float: left">
                      <el-badge value="hot" class="menu-badge">
                        <el-button style="width: 140px" type="primary" plain :icon="i ? 'el-icon-medal' : 'el-icon-medal-1'" @click="test(item)">
                          <div class="text" style="max-width:100px;display: inline-block" :title="item">{{ item }}</div>
                        </el-button>
                      </el-badge>
                    </div>
                    <el-button style="width: 140px;height: 33.3px;top: 11px;position: relative;" type="primary" plain @click="test('交割货款支付')">
                      <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                      交割货款支付
                    </el-button>
                  </div>
                  <div class="dis-flex" style="width: 100%;margin-bottom: 10px;">
                    <!--                  <div v-for="(item, i) in menuList1" :key="'menu1' + i" style="width: 33%; float: left">-->
                    <!--                    <el-button type="primary" plain icon="el-icon-star-off" @click="test(item)">-->
                    <!--                      {{ item }}-->
                    <!--                    </el-button>-->
                    <!--                  </div>-->
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain icon="el-icon-star-off" @click="test('交割通知单')">
                        交割通知单
                      </el-button>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain @click="test('交割货款支付')">
                        <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                        交割货款支付
                      </el-button>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-popover
                        placement="right"
                        trigger="hover">
                        <span style="font-size: 12px;color: #aaa" @click="toggleHuiyuanIcon" class="hand hand-underline">{{ huiyuanicon?'点击取消收藏':'点击收藏' }}</span>
                        <el-button style="width: 140px" slot="reference" type="primary" plain :icon="{'el-icon-star-on':huiyuanicon,'el-icon-star-off':!huiyuanicon}" @click="test('会员结算业务')">
                          会员结算业务
                        </el-button>
                      </el-popover>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain @click="test('交割货款支付')">
                        <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                        交割货款支付
                      </el-button>
                    </div>
                  </div>
                  <div class="dis-flex" style="width: 100%;margin-bottom: 10px;">
                    <div v-for="(item, i) in menuList2" :key="'menu2' + i" style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain icon="el-icon-star-on" @click="test(item)">
                        <div class="text" style="max-width:100px;display: inline-block" :title="item">{{ item }}</div>
                      </el-button>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain @click="test('交割货款支付')">
                        <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                        交割货款支付
                      </el-button>
                    </div>
                  </div>
                  <div class="dis-flex" style="width: 100%;margin-bottom: 10px;">
                    <!--                  <div v-for="(item, i) in menuList1" :key="'menu1' + i" style="width: 33%; float: left">-->
                    <!--                    <el-button type="primary" plain icon="el-icon-star-off" @click="test(item)">-->
                    <!--                      {{ item }}-->
                    <!--                    </el-button>-->
                    <!--                  </div>-->
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain icon="el-icon-star-off" @click="test('交割通知单')">
                        交割通知单
                      </el-button>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain @click="test('交割货款支付')">
                        <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                        交割货款支付
                      </el-button>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-popover
                        placement="right"
                        trigger="hover">
                        <span style="font-size: 12px;color: #aaa" @click="toggleHuiyuanIcon" class="hand hand-underline">{{ huiyuanicon?'点击取消收藏':'点击收藏' }}</span>
                        <el-button style="width: 140px" slot="reference" type="primary" plain :icon="{'el-icon-star-on':huiyuanicon,'el-icon-star-off':!huiyuanicon}" @click="test('会员结算业务')">
                          会员结算业务
                        </el-button>
                      </el-popover>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain icon="el-icon-star-off" @click="test('交割通知单')">
                        交割通知单
                      </el-button>
                    </div>
                  </div>
                  <div class="dis-flex" style="width: 100%;margin-bottom: 10px;">
                    <div v-for="(item, i) in menuList2" :key="'menu2' + i" style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain icon="el-icon-star-on" @click="test(item)">
                        <div class="text" style="max-width:100px;display: inline-block" :title="item">{{ item }}</div>
                      </el-button>
                    </div>
                    <div style="width: 25%; float: left">
                      <el-button style="width: 140px" type="primary" plain @click="test('交割货款支付')">
                        <i :class="{'el-icon-star-on':jiaogeicon,'el-icon-star-off':!jiaogeicon}" @click.stop="toggleJiaogeIcon" />
                        交割货款支付
                      </el-button>
                    </div>
                  </div>
                </el-scrollbar>
              </div>
            </transition>
          </div>
        </div>
        <!-- 日历提醒 -->
        <div class="dis-flex" style="width: 100%; height: 700px;">
          <div style="width: 100%;height: 25px;font-size: 18px;font-weight: 700;margin-top: 10px;">
            个人提醒
            <el-tooltip class="item" effect="dark" content="双击日期可新增提醒事项" placement="top-end">
              <i class="el-icon-info" />
            </el-tooltip>
          </div>
          <div style="width: 50%; height: 100%">
            <el-calendar v-model="calendarDay">
              <template slot="dateCell" slot-scope="{date, data}">
                <span :class="{'is-selected':data.isSelected}">
                  <span :class="showDot(data)" @dblclick="showNewDialog(data)">
                    {{ data.day.split('-')[2] }}
                  </span>
                </span>
              </template>
            </el-calendar>
          </div>
          <div style="width: 50%; height: 100%">
            <div style="width: 100%;height: 230px;padding: 10px 0 0 10px">
              <div class="dis-flex-bet" style="width: 100%;height: 25px;">
                <div style="width: 49%;font-size: 14px;line-height: 25px;">
                  <i class="el-icon-success" style="color: #42b983; top: 3px" />
                  已完成:
                  <el-dropdown>
                    <span trigger="click" class="el-dropdown-link" style="font-size: 20px;line-height: 25px;margin-left: 10px;">
                      3 项
                      <i class="el-icon-arrow-down el-icon--right" />
                    </span>
                    <el-dropdown-menu slot="dropdown">
                      <el-dropdown-item>交割账户资金划转申请 - 20220901</el-dropdown-item>
                      <el-dropdown-item>国债充出 - 20220902</el-dropdown-item>
                      <el-dropdown-item>席位申请 - 20220903</el-dropdown-item>
                    </el-dropdown-menu>
                  </el-dropdown>
                </div>
                <div style="width: 49%;font-size: 14px;line-height: 25px;">
                  <i class="el-icon-refresh" style="color: coral; top: 3px" />
                  未完成:
                  <el-dropdown>
                    <span trigger="click" class="el-dropdown-link" style="font-size: 20px;line-height: 25px;margin-left: 10px;">
                      5 项
                      <i class="el-icon-arrow-down el-icon--right" />
                    </span>
                    <el-dropdown-menu slot="dropdown">
                      <el-dropdown-item>席位撤销 - 20220901</el-dropdown-item>
                      <el-dropdown-item>专线密码修改 - 20220902</el-dropdown-item>
                      <el-dropdown-item>套期保值交易资格申请 - 20220903</el-dropdown-item>
                      <el-dropdown-item>经营规模或需求额度申请 - 20220903</el-dropdown-item>
                      <el-dropdown-item>投保互换申请 - 20220903</el-dropdown-item>
                    </el-dropdown-menu>
                  </el-dropdown>
                </div>
              </div>
              <div style="width: 100%; height: 160px;margin-top: 42px">
                <div style="margin-bottom: 5px">
                  {{ formatDate(calendarDay, "yyyy-MM-dd") }}
                </div>
                <div v-if="formatDay===today">
                  <transition name="el-fade-in-linear">
                    <div v-show="calendarVisible">
                      <div v-for="(item, i) in calendarList1" :key="'calendar' + i" style="font-size: 12px; color: #303133; margin-top: 15px" class="hand hand-underline" @click="showEditDialog(i)">
                        <i v-if="item.status == 'done'" class="el-icon-success" style="color: #42b983; top: 3px" />
                        <i v-else class="el-icon-refresh" style="color: coral; top: 3px" />
                        <span class="text" :title="item.title" style="display:inline-block;width: 230px;line-height: 14px;height: 14px;margin-left: 3px;padding-top: 3px;">
                          {{ item.title }}
                        </span>
                      </div>
                    </div>
                  </transition>
                </div>
                <div v-else-if="formatDay==='2022-09-02'">
                  <transition  name="el-fade-in-linear">
                    <div v-show="calendarVisible">
                      <img src="./nodata1.png" width="240px" height="210px">
                    </div>
                  </transition>
                </div>
                <div v-else>
                  <transition  name="el-fade-in-linear">
                    <div v-show="calendarVisible">
                      <div v-for="(item, i) in calendarList0" :key="'calendar' + i" style="font-size: 12px; color: #303133; margin-top: 15px" class="hand hand-underline">
                        <i v-if="item.status == 'done'" class="el-icon-success" style="color: #42b983; top: 3px" />
                        <i v-else class="el-icon-refresh" style="color: coral; top: 3px" />
                        {{ item.title }}
                      </div>
                    </div>
                  </transition>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div style="width: 28%; height: 100%; padding-left: 5px">
        <!-- 用户信息 -->
        <div style="height: 55px;width: 100%;border-bottom: 1px solid #eee;display: flex;margin: 0 0 25px 0;">
          <div style="width: 45px;height: 45px;border-radius: 20px;background-color: antiquewhite;">
            <i class="el-icon-user-solid" style="color: white; font-size: 30px;margin:6px 0 0 7px" />
          </div>
          <div style="width: 200px; height: 40px; margin-left: 15px">
            <div style="height: 20px">业务产品部 - mujian</div>
            <div style="height: 20px;font-size: 13px;margin-top: 4px;color: #aaa">
              欢迎使用业务管理系统!
            </div>
          </div>
        </div>
        <!-- 近7日待办 -->
        <div style="height: 240px;width: 100%;border-bottom: 1px solid #eee;margin: 23px 0;">
          <div class="dis-flex-bet" style="height: 25px;line-height: 15px;width: 100%">
            <span>
              <el-badge value="13" class="daibanbadge">
                <span style="font-size: 18px; color: #303133; font-weight: 700;margin-right: 5px">
                  待办事项(体验)
                </span>
              </el-badge>
<!--              <span style="font-size: 12px; color: #aaa" class="hand hand-underline" title="刷新" @click="test('刷新')">-->
<!--                <i class="el-icon-refresh-right" />-->
<!--              </span>-->
            </span>
            <span style="font-size: 12px; color: #aaa" class="hand hand-underline" @click="test('MORE')">MORE</span>
          </div>
          <div style="width: 95%; font-size: 14px; color: #303133">
            <el-scrollbar style="height:200px" wrap-style="overflow-x:hidden;">
              <div v-for="(item, i) in todoList" :key="'todo' + i" class="dis-flex-bet" style="margin-top: 6px;padding-right: 10px">
                <div class="hand" @click="test(item.title)">
                  <i class="el-icon-position" style="font-size: 12px; top: 2px; right: 4px" />
                  <div style="display: inline-block;margin-left: 3px" class="todo">
                    {{ item.title }}
                  </div>
                </div>
                <div style="color: #aaa; font-size: 11px">
                  {{ "( " + item.count + " )" }}
                </div>
              </div>
            </el-scrollbar>
          </div>
        </div>
        <!-- 系统消息 -->
        <div style="height: 300px;width: 100%;border-bottom: 1px solid #eee;margin-top: 25px;">
          <div class="dis-flex-bet" style="height: 25px;line-height: 15px;width: 100%;">
            <span style="font-size: 18px; color: #303133; font-weight: 700">
              系统消息
              <span style="font-size: 12px; color: #aaa" class="hand hand-underline" title="刷新" @click="test('刷新')">
                <i class="el-icon-refresh-right" />
              </span>
            </span>
            <span style="font-size: 12px; color: #aaa" class="hand hand-underline" @click="test('MORE')">
              MORE
            </span>
          </div>
          <div style="width: 100%; font-size: 14px; color: #303133">
            <div v-for="(item, i) in systemList" :key="'system' + i" class="dis-flex-bet" style="margin-top: 6px;">
              <div class="hand" @click="test(item.title)">
                <i class="el-icon-chat-line-square" style="font-size: 12px; top: 2px; right: 4px" />
                <div style="display: inline-block;margin-left: 3px" class="todo">
                  {{ item.title }}
                </div>
              </div>
              <div style="color: #aaa; font-size: 11px">
                {{ item.date }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <el-dialog :title="dialogTitle" :visible.sync="dialogVisible" width="400px" :close-on-click-modal="false">
      <el-row style="margin-bottom: 10px">
        <el-input v-model="newCalendarTitle" size="small" style="width: 289px" maxlength="100" show-word-limit>
          <template slot="prepend">提醒事项:</template>
        </el-input>
      </el-row>
      <el-row style="display: flex">
        <div class="el-input-group__prepend" style="width: 96px;line-height: 30px">事项状态:</div>
        <el-select v-model="newCalendarStatus" placeholder="请选择">
          <el-option label="已完成" value="done">
            <span><i class="el-icon-success" style="color: #42b983; top: 3px;right: 3px" />
              已完成
            </span>
          </el-option>
          <el-option label="未完成" value="todo">
            <span>
              <i class="el-icon-refresh" style="color: coral; top: 3px" />
              未完成
            </span>
          </el-option>
        </el-select>
      </el-row>
      <el-row style="text-align: center;margin-top: 20px">
        <span v-if="newCalendarIndex>=0" style="margin-right: 20px">
          <el-popconfirm title="您确定删除该提醒事项吗?" @onConfirm="delCalendar">
            <el-button slot="reference" type="danger">删除</el-button>
          </el-popconfirm>
        </span>
        <el-button @click="updateCalendar" type="primary">确定</el-button>
      </el-row>
    </el-dialog>
  </el-card>
</template>

<script>
export default {
  data() {
    return {
      calendarDay: new Date(),
      todoList: [
        {
          title: '品种A手续费变更',
          date: '20220904',
          count: '2'
        },
        {
          title: '会员0019申请境外期货业务',
          date: '20220905',
          count: '4'
        },
        {
          title: '推进铂、钯期货品种研发',
          date: '20220906',
          count: '1'
        },
        {
          title: '铁矿石期权上市路演',
          date: '20220908',
          count: '7'
        },
        {
          title: '会员0019申请境外期货业务',
          date: '20220905',
          count: '1'
        },
        {
          title: '推进铂、钯期货品种研发',
          date: '20220906',
          count: '3'
        },
        {
          title: '品种A手续费变更',
          date: '20220904',
          count: '2'
        },
        {
          title: '会员0019申请境外期货业务',
          date: '20220905',
          count: '4'
        },
        {
          title: '推进铂、钯期货品种研发',
          date: '20220906',
          count: '1'
        },
        {
          title: '铁矿石期权上市路演',
          date: '20220908',
          count: '7'
        },
        {
          title: '会员0019申请境外期货业务',
          date: '20220905',
          count: '1'
        },
        {
          title: '推进铂、钯期货品种研发',
          date: '20220906',
          count: '3'
        },
        {
          title: '品种A手续费变更',
          date: '20220904',
          count: '2'
        },
        {
          title: '会员0019申请境外期货业务',
          date: '20220905',
          count: '4'
        },
        {
          title: '推进铂、钯期货品种研发',
          date: '20220906',
          count: '1'
        },
        {
          title: '铁矿石期权上市路演',
          date: '20220908',
          count: '7'
        },
        {
          title: '会员0019申请境外期货业务',
          date: '20220905',
          count: '1'
        },
        {
          title: '推进铂、钯期货品种研发',
          date: '20220906',
          count: '3'
        }
      ],
      systemList: [
        {
          title: '清算系统消息',
          date: '20220811 11:15:20'
        },
        {
          title: '频繁报撤单超限预警',
          date: '20220811 09:54:11'
        },
        {
          title: '清算系统消息',
          date: '20220810 11:15:20'
        },
        {
          title: '异常交易通知',
          date: '20220808 14:31:17'
        },
        {
          title: '自成交超限预警',
          date: '20220807 10:30:22'
        },
        {
          title: '频繁报撤单超限预警',
          date: '20220805 09:54:11'
        },
        {
          title: '大额报撤单超限预警',
          date: '20220804 14:31:17'
        },
        {
          title: '异常交易通知',
          date: '20220803 14:31:17'
        },
        {
          title: '清算系统消息',
          date: '20220802 11:15:20'
        },
        {
          title: '自成交超限预警',
          date: '20220801 10:30:22'
        }
      ],
      menuList0: ['保证金优惠参数表', '成交持仓表', '仓储费相关信息表'],
      menuList1: ['交割通知单', '交割货款支付', '会员结算业务'],
      menuList2: ['国债充抵保证金国债充抵保证金国债充抵保证金国债充抵保证金国债充抵保证金国债充抵保证金国债充抵保证金国债充抵保证金国债充抵保证金', '充抵调整', '充抵合同详情'],
      menuVisible: true,
      calendarList0: [
        {
          status: 'done',
          title: '交割账户资金划转申请&充抵保证金补缴'
        },
        {
          status: 'done',
          title: '套期保值交易资格申请'
        },
        {
          status: 'todo',
          title: '经营规模或品种模式需求额度申请'
        }
      ],
      calendarList1: [
        {
          status: 'done',
          title: '套期保值交易资格申请套期保值交易资格申请套期保值交易资格申请套期保值交易资格申请套期保值交易资格申请'
        },
        {
          status: 'todo',
          title: '经营规模或品种模式需求额度申请'
        }
      ],
      calendarVisible: true,
      calendarDayDoneList: ['2022-09-01', '2022-09-05', '2022-09-12'],
      calendarDayTodoList: ['2022-09-12', '2022-09-20', '2022-09-29'],
      dialogVisible: false,
      dialogTitle: '',
      newCalendarTitle: '',
      newCalendarStatus: '',
      newCalendarIndex: -1,
      today: '2022-09-15',
      formatDay: '',
      jiaogeicon: true,
      huiyuanicon: false,
      huiyuanIconVisible: false,
      menuLayout: '3x3'
    }
  },
  watch: {
    calendarDay(n, o) {
      this.formatDay = this.formatDate(n)
      this.calendarVisible = false
      setTimeout(() => {
        this.calendarVisible = true
      }, 500)
    }
  },
  mounted() {
    // this.initMenu()
  },
  methods: {
    test(type = 'default') {
      this.$message(type)
    },
    refreshMenu() {
      this.menuVisible = false
      setTimeout(() => {
        this.menuVisible = true
      }, 1000)
    },
    formatDate(date, fmt = 'yyyy-MM-dd') {
      if (/(y+)/.test(fmt)) {
        fmt = fmt.replace(
          RegExp.$1,
          (date.getFullYear() + '').substr(4 - RegExp.$1.length)
        )
      }
      const o = {
        'M+': date.getMonth() + 1,
        'd+': date.getDate(),
        'h+': date.getHours(),
        'm+': date.getMinutes(),
        's+': date.getSeconds()
      }
      for (const k in o) {
        if (new RegExp(`(${k})`).test(fmt)) {
          const str = o[k] + ''
          fmt = fmt.replace(
            RegExp.$1,
            RegExp.$1.length === 1 ? str : this.padLeftZero(str)
          )
        }
      }
      return fmt
    },
    padLeftZero(str) {
      return ('00' + str).substr(str.length)
    },
    showDot(data) {
      if (data.day === this.today) {
        return 'todo-dot done-dot1'
      }
      const todoDot = this.showTodoDot(data)
      const doneDot = this.showDoneDot(data)
      if (todoDot && doneDot) {
        return 'todo-dot done-dot1'
      } else {
        if (todoDot) {
          return 'todo-dot'
        }
        if (doneDot) {
          return 'done-dot'
        }
      }
    },
    showTodoDot(data) {
      if (this.calendarDayTodoList.indexOf(data.day) >= 0) {
        return true
      } else {
        return false
      }
    },
    showDoneDot(data) {
      if (this.calendarDayDoneList.indexOf(data.day) >= 0) {
        return true
      } else {
        return false
      }
    },
    showNewDialog(data) {
      this.dialogTitle = data.day + ' - 新增'
      this.dialogVisible = true
    },
    showEditDialog(i) {
      this.dialogTitle = this.today + ' - 修改'
      this.newCalendarTitle = this.calendarList1[i].title
      this.newCalendarStatus = this.calendarList1[i].status
      this.newCalendarIndex = i
      this.dialogVisible = true
    },
    updateCalendar() {
      if (this.newCalendarIndex >= 0) {
        // 修改
        this.calendarList1.splice(this.newCalendarIndex, 1, {
          title: this.newCalendarTitle,
          status: this.newCalendarStatus
        })
      } else {
        this.calendarList1.push({
          title: this.newCalendarTitle,
          status: this.newCalendarStatus
        })
      }
      this.newCalendarTitle = ''
      this.newCalendarStatus = ''
      this.newCalendarIndex = -1
      this.dialogVisible = false
    },
    delCalendar() {
      this.calendarList1.splice(this.newCalendarIndex, 1)
      this.newCalendarTitle = ''
      this.newCalendarStatus = ''
      this.newCalendarIndex = -1
      this.dialogVisible = false
    },
    toggleJiaogeIcon() {
      let mess = ''
      if (this.jiaogeicon) {
        mess = '取消'
      } else {
        mess = '已'
      }
      this.jiaogeicon = !this.jiaogeicon
      this.$message(mess + '收藏')
    },
    toggleHuiyuanIcon() {
      let mess = ''
      if (this.huiyuanicon) {
        mess = '取消'
      } else {
        mess = '已'
      }
      this.$message(mess + '收藏')
      this.huiyuanicon = !this.huiyuanicon
    },
    handleCommand(command) {
      this.menuVisible = false

      setTimeout(() => {
        this.menuLayout = command
        this.menuVisible = true
      }, 500)
    }
  }
}
</script>
<style scoped lang="scss">
.hand {
  cursor: pointer
}

.hand-underline {
  &:hover{
    text-decoration: underline;
  }
}

.todo {
  &:hover{
    transform: scale(1.05);
  }
}

.menu-badge {
  margin-top: 10px;
  margin-right: 40px;
}

.clear-title::before {
  content: "";
  display: block;
  position: absolute;
  width: 6px;
  height: 14px;
  top: 3px;
  left: -10px;
  border-radius: 5px;
  background: #6495ed6e;
}
.is-selected {
  color: #1989FA;
}
.dis-flex{
  display: flex;
  flex-wrap: wrap;
}
.dis-flex-bet{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.todo-dot{
  position: relative;
  &:after{
    content: "";
    display: block;
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 2px;
    top: 20px;
    left: 6px;
    border-radius: 5px;
    background: coral;
  }
}
.done-dot{
  position: relative;
  &:after{
    content: "";
    display: block;
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 2px;
    top: 20px;
    left: 8px;
    border-radius: 5px;
    background: #42b983;
  }
}
.done-dot1{
  position: relative;
  &:before{
    content: "";
    display: block;
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 2px;
    top: 20px;
    left: 14px;
    border-radius: 5px;
    background: #42b983;
  }
}
.dropdown-dot{
  position: relative;
  &:before{
    content: "";
    display: block;
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 2px;
    top: 10px;
    left: 7px;
    border-radius: 5px;
    background: #6cadc8ee;
  }
}
.text{
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.daibanbadge{
  //top: 3px;
}
</style>
<style lang="scss">
>>>.el-carousel__button {
  background-color: #aaa;
}
.el-calendar-table .el-calendar-day{
  height: 35px !important;
}
.el-popover.el-popper{
  min-width: 80px!important;
}
#favMenu {
  .el-button.el-button--primary.el-button--small.is-plain{
    text-align: left;
  }
}
</style>
