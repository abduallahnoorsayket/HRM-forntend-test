<template>
  <div class="app-sidebar sidebar-shadow">
    <div class="app-header__logo">
      <div class="logo-src"></div>
      <div class="header__pane ml-auto">
        <div>
          <button
            type="button"
            class="hamburger close-sidebar-btn hamburger--elastic"
            data-class="closed-sidebar"
          >
            <span class="hamburger-box">
              <span class="hamburger-inner"></span>
            </span>
          </button>
        </div>
      </div>
    </div>
    <div class="app-header__mobile-menu">
      <div>
        <button
          type="button"
          class="hamburger hamburger--elastic mobile-toggle-nav"
        >
          <span class="hamburger-box">
            <span class="hamburger-inner"></span>
          </span>
        </button>
      </div>
    </div>
    <div class="app-header__menu">
      <span>
        <button
          type="button"
          class="btn-icon btn-icon-only btn btn-primary btn-sm mobile-toggle-header-nav"
        >
          <span class="btn-icon-wrapper">
            <i class="fa fa-ellipsis-v fa-w-6"></i>
          </span>
        </button>
      </span>
    </div>

    <!--Sidebar Menu Start-->
    <div class="scrollbar-sidebar">
      <div class="app-sidebar__inner">
        <!-- new dashboard menu -->
        <ul class="vertical-nav-menu mt-2">
          <li>
            <router-link
              :to="{ path: '/dashboard' }"
              :class="{ 'mm-active': currentRoutePath(['/dashboard']) }"
            >
              <i class="metismenu-icon pe-7s-timer"></i>
              {{ $store.getters.GET_DASHBOARD }}
            </router-link>
          </li>
        </ul>
        <!-- new dashboard menu  end-->
        <!-- demo Menu start -->
        <!-- demo Menu end -->
        <nav>
          <ul class="vertical-nav-menu mt-0">
            <li
              v-if="hasModulePermission('auth', 'hrm_auth')"
              class="app-sidebar__heading"
            >
              {{ $store.getters.GET_BASE }}
              <br />
              <!-- ß{{currentRoutePath ('/create-new-user')}} -->
            </li>
            <!--users-->
            <li
              v-if="hasModelPermission('user')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-new-user',
                  '/user-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="currentRoutePath(['/create-new-user', '/user-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-users"></i>
                    {{ $store.getters.GET_USER }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <!-- <a @click="OpenMenu($event)">
                  <i class="metismenu-icon pe-7s-users"></i>
                  {{ $store.getters.GET_USER }}
                  <i
                    class="metismenu-state-icon pe-7s-angle-down caret-left"
                  ></i>
                </a> -->
                <ul>
                  <li v-if="hasPermission('add_user')">
                    <router-link
                      :to="{ path: '/create-new-user' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-new-user']),
                      }"
                    >
                      {{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>
                  <li v-if="hasPermission('view_user')">
                    <router-link
                      :to="{ path: '/user-list' }"
                      :class="{ 'mm-active': currentRoutePath(['/user-list']) }"
                    >
                      {{ $store.getters.GET_LIST }}</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
            <!--Groups-->
            <li
              v-if="hasModelPermission('group')"
              class="mt-0"
              :class="{
                'mm-active': currentRoutePath(['/create-group', '/group-list']),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="currentRoutePath(['/create-group', '/group-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon fas pe-7s-id"></i>
                    {{ $store.getters.GET_GROUP }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <!--add_group-->
                  <li v-if="hasPermission('add_group')">
                    <router-link
                      :to="{ path: '/create-group' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-group']),
                      }"
                    >
                      {{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>

                  <!--view_group-->
                  <li v-if="hasPermission('view_group')">
                    <router-link
                      :to="{ path: '/group-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/group-list']),
                      }"
                    >
                      {{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!-- Department -->
            <li
              v-if="hasModelPermission('department')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-department',
                  '/department-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath(['/create-department', '/department-list'])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon fas pe-7s-photo-gallery"></i>
                    {{ $store.getters.GET_DEPARTMENT }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <!-- <a @click="OpenMenu($event)">
                  <i class="metismenu-icon pe-7s-users"></i>
                  {{ $store.getters.GET_USER }}
                  <i
                    class="metismenu-state-icon pe-7s-angle-down caret-left"
                  ></i>
                </a> -->
                <ul>
                  <li v-if="hasPermission('add_department')">
                    <router-link
                      :to="{ path: '/create-department' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-department']),
                      }"
                      >{{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>
                  <li v-if="hasPermission('view_department')">
                    <router-link
                      :to="{ path: '/department-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/department-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!-- Branch -->
            <li
              v-if="hasModelPermission('branch')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-branch',
                  '/branch-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="currentRoutePath(['/create-branch', '/branch-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-network"></i>
                    {{ $store.getters.GET_BRANCH }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_branch')">
                    <router-link
                      :to="{ path: '/create-branch' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-branch']),
                      }"
                      >{{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>

                  <li v-if="hasPermission('view_branch')">
                    <router-link
                      :to="{ path: '/branch-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/branch-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!-- Designation -->
            <li
              v-if="hasModelPermission('designation')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-designation',
                  '/designation-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath(['/create-designation', '/designation-list'])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-shopbag"></i>
                    {{ $store.getters.GET_DESIGNATION }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_designation')">
                    <router-link
                      :to="{ path: '/create-designation' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-designation']),
                      }"
                      >{{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>
                  <li v-if="hasPermission('view_designation')">
                    <router-link
                      :to="{ path: '/designation-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/designation-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
          </ul>
          <ul class="vertical-nav-menu mt-0">
            <li
              v-if="hasModulePermission('hrm_attendance')"
              class="app-sidebar__heading"
            >
              {{ $store.getters.GET_ATTENDANCE }}
              <br />
            </li>
            <!--New attendance records-->
            <!--   v-if="hasModelPermission('user')" -->
            <li
              :class="{
                'mm-active': currentRoutePath([
                  '/all-attendance-records',
                  '/my-attendance-records',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath([
                    '/all-attendance-records',
                    '/my-attendance-records',
                  ])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-news-paper"></i>
                    {{
                      $store.getters.GET_ATTENDANCE +
                      " " +
                      $store.getters.GET_RECORD
                    }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('view_attendancerecord')">
                    <router-link
                      :to="{ path: '/all-attendance-records' }"
                      :class="{
                        'mm-active': currentRoutePath([
                          '/all-attendance-records',
                        ]),
                      }"
                    >
                      <i class="metismenu-icon pe-7s-news-paper"></i>
                      {{
                        $store.getters.GET_ALL +
                        " " +
                        $store.getters.GET_ATTENDANCE
                      }}
                    </router-link>
                  </li>
                  <li>
                    <router-link
                      :to="{ path: '/my-attendance-records' }"
                      :class="{
                        'mm-active': currentRoutePath([
                          '/my-attendance-records',
                        ]),
                      }"
                      >{{
                        $store.getters.GET_MY +
                        " " +
                        $store.getters.GET_ATTENDANCE
                      }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!-- holiday -->
            <li
              v-if="hasModelPermission('holiday')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-holiday',
                  '/holiday-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="currentRoutePath(['/create-holiday', '/holiday-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-coffee"></i>
                    {{ $store.getters.GET_HOLIDAY }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_holiday')">
                    <router-link
                      :to="{ path: '/create-holiday' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-holiday']),
                      }"
                      >{{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>

                  <li v-if="hasPermission('view_holiday')">
                    <router-link
                      :to="{ path: '/holiday-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/holiday-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!--Branch Holiday-->
            <li
              v-if="hasModelPermission('branchholiday')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-branch-holiday',
                  '/branch-holiday-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath([
                    '/create-branch-holiday',
                    '/branch-holiday-list',
                  ])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-map-2"></i>
                    {{
                      $store.getters.GET_BRANCH +
                      " " +
                      $store.getters.GET_HOLIDAY
                    }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_branchholiday')">
                    <router-link
                      :to="{ path: '/create-branch-holiday' }"
                      :class="{
                        'mm-active': currentRoutePath([
                          '/create-branch-holiday',
                        ]),
                      }"
                      >{{ $store.getters.GET_CREATE }}</router-link
                    >
                  </li>

                  <li v-if="hasPermission('view_branchholiday')">
                    <router-link
                      :to="{ path: '/branch-holiday-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/branch-holiday-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
            <!--Leave Type-->
            <li
              v-if="hasModelPermission('leavetype')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-leave-types',
                  '/leave-types',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath(['/create-leave-types', '/leave-types'])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-bandaid"></i>
                    {{
                      $store.getters.GET_LEAVE + " " + $store.getters.GET_TYPE
                    }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_leavetype')">
                    <router-link
                      :to="{ path: '/create-leave-types' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-leave-types']),
                      }"
                      >{{ $store.getters.GET_CREATE }}</router-link
                    >
                  </li>

                  <li v-if="hasPermission('view_leavetype')">
                    <router-link
                      :to="{ path: '/leave-types' }"
                      :class="{
                        'mm-active': currentRoutePath(['/leave-types']),
                      }"
                      >{{ $store.getters.GET_LIST }}</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
            <!--All Leave-->
            <li
              :class="{
                'mm-active': currentRoutePath([
                  '/add-leaves-request',
                  '/all-leaves',
                  '/my-leaves',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath([
                    '/add-leaves-request',
                    '/all-leaves',
                    '/my-leaves',
                  ])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-paperclip"></i>
                    {{ $store.getters.GET_LEAVE }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_leave')">
                    <router-link
                      :to="{ path: '/add-leaves-request' }"
                      :class="{
                        'mm-active': currentRoutePath(['/add-leaves-request']),
                      }"
                      >{{ $store.getters.GET_CREATE }}</router-link
                    >
                  </li>

                  <li v-if="hasPermission('view_leave')">
                    <router-link
                      :to="{ path: '/all-leaves' }"
                      :class="{
                        'mm-active': currentRoutePath(['/all-leaves']),
                      }"
                      >{{
                        $store.getters.GET_ALL + " " + $store.getters.GET_LEAVES
                      }}
                    </router-link>
                  </li>
                  <!--My Leave History & my leave list-->
                  <li>
                    <router-link
                      :to="{ path: '/my-leaves' }"
                      :class="{ 'mm-active': currentRoutePath(['/my-leaves']) }"
                    >
                      <i class="metismenu-icon pe-7s-back-2"></i>
                      {{
                        $store.getters.GET_MY + " " + $store.getters.GET_LEAVES
                      }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
          </ul>
          <ul class="vertical-nav-menu mt-0">
            <li
              v-if="hasModulePermission('hrm_evaluation')"
              class="app-sidebar__heading"
            >
              {{ $store.getters.GET_EVALUATION }}
              <br />
            </li>
            <!-- rating -->
            <li
              v-if="hasModelPermission('rating')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-rating',
                  '/rating-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="currentRoutePath(['/create-rating', '/rating-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-star"></i>
                    {{ $store.getters.GET_RATING }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_rating')">
                    <router-link
                      :to="{ path: '/create-rating' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-rating']),
                      }"
                      >{{ $store.getters.GET_CREATE }}</router-link
                    >
                  </li>

                  <li v-if="hasPermission('view_rating')">
                    <router-link
                      :to="{ path: '/rating-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/rating-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
            <!-- rating point-->
            <li
              v-if="hasModelPermission('ratingpoint')"
              :class="{
                'mm-active': currentRoutePath([
                  '/create-rating-point',
                  '/rating-point-list',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath([
                    '/create-rating-point',
                    '/rating-point-list',
                  ])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-graph2"></i>
                    {{
                      $store.getters.GET_RATING + " " + $store.getters.GET_POINT
                    }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_ratingpoint')">
                    <router-link
                      :to="{ path: '/create-rating-point' }"
                      :class="{
                        'mm-active': currentRoutePath(['/create-rating-point']),
                      }"
                      >{{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>

                  <li v-if="hasPermission('view_ratingpoint')">
                    <router-link
                      :to="{ path: '/rating-point-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/rating-point-list']),
                      }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!--Add Evaluation-->
            <li
              v-if="
                hasModelPermission('evaluation') &&
                hasPermission('add_evaluation')
              "
            >
              <router-link
                :to="{ path: '/add-evaluation' }"
                :class="{ 'mm-active': currentRoutePath(['/add-evaluation']) }"
              >
                <i class="metismenu-icon pe-7s-note2"></i>
                {{
                  $store.getters.GET_ADD + " " + $store.getters.GET_EVALUATION
                }}
              </router-link>
            </li>
            <!--Evaluation Graph-->
            <li
              :class="{
                'mm-active': currentRoutePath([
                  '/evaluation-graph',
                  '/my-evaluation',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath(['/evaluation-graph', '/my-evaluation'])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-graph1"></i>
                    {{ $store.getters.GET_EVALUATION }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('view_evaluation')">
                    <router-link
                      :to="{ path: '/evaluation-graph' }"
                      :class="{
                        'mm-active': currentRoutePath(['/evaluation-graph']),
                      }"
                      >{{
                        $store.getters.GET_EVALUATION +
                        " " +
                        $store.getters.GET_GRAPH
                      }}
                    </router-link>
                  </li>

                  <!-- <li
                v-if="hasPermission('view_employeeinformation') && hasPermission('view_employeerating')"
              >
                <router-link
                  :to="{ path: '/department-wise' }"
                  :class="{'mm-active' : currentRoutePath(['/department-wise'])}"
                >Department Wise</router-link>
              </li> -->

                  <li>
                    <router-link
                      :to="{ path: '/my-evaluation' }"
                      :class="{
                        'mm-active': currentRoutePath(['/my-evaluation']),
                      }"
                      >{{
                        $store.getters.GET_MY +
                        " " +
                        $store.getters.GET_EVALUATION
                      }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
          </ul>
          <!--Project  realted new Start-->
          <!-- <ul class="vertical-nav-menu mt-0">
            <li
              class="app-sidebar__heading"
              v-if="hasModulePermission('hrm_project')"
            >
              Project Related
              <br />
            </li>
            
            <li
              v-if="hasModelPermission('client')"
              :class="{
                'mm-active': currentRoutePath(['/add-client', '/client-list']),
              }"
            >
              
              <details
                class="dropdown"
                :open="currentRoutePath(['/add-client', '/client-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-user"></i>
                    Client
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_client')">
                    <router-link
                      :to="{ path: '/add-client' }"
                      :class="{
                        'mm-active': currentRoutePath(['/add-client']),
                      }"
                      >Add Client</router-link
                    >
                  </li>
                  <li v-if="hasPermission('view_client')">
                    <router-link
                      :to="{ path: '/client-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/client-list']),
                      }"
                      >Client list</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
            
            <li
              v-if="hasModelPermission('project')"
              :class="{
                'mm-active': currentRoutePath([
                  '/add-new-project',
                  '/project-list',
                ]),
              }"
            >
              
              <details
                class="dropdown"
                :open="currentRoutePath(['/add-new-project', '/project-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-drawer"></i>
                    Projects
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_project')">
                    <router-link
                      :to="{ path: '/add-new-project' }"
                      :class="{
                        'mm-active': currentRoutePath(['/add-new-project']),
                      }"
                      >Add New Project</router-link
                    >
                  </li>
                  <li v-if="hasPermission('view_project')">
                    <router-link
                      :to="{ path: '/project-list' }"
                      :class="{
                        'mm-active': currentRoutePath(['/project-list']),
                      }"
                      >Project list</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
            
            <li
              v-if="
                hasPermission('view_worktype') ||
                hasPermission('view_workstatus') ||
                hasPermission('view_workpriority')
              "
              :class="{
                'mm-active': currentRoutePath([
                  '/work-type',
                  '/work-status',
                  '/work-priority',
                ]),
              }"
            >
              
              <details
                class="dropdown"
                :open="
                  currentRoutePath([
                    '/work-type',
                    '/work-status',
                    '/work-priority',
                  ])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-drawer"></i>
                    All Category
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('view_worktype')">
                    <router-link
                      :to="{ path: '/work-type' }"
                      :class="{ 'mm-active': currentRoutePath(['/work-type']) }"
                      >Work Type</router-link
                    >
                  </li>

                  <li v-if="hasPermission('view_workstatus')">
                    <router-link
                      :to="{ path: '/work-status' }"
                      :class="{
                        'mm-active': currentRoutePath(['/work-status']),
                      }"
                      >Work Status</router-link 
                    >
                  </li>

                  <li v-if="hasPermission('view_workpriority')">
                    <router-link
                      :to="{ path: '/work-priority' }"
                      :class="{
                        'mm-active': currentRoutePath(['/work-priority']),
                      }"
                      >Work Priority</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
          </ul> -->
          <!-- project related end -->
          <!--Project  realted old Start-->
          <!-- <ul class="vertical-nav-menu">
          <li
            v-if="hasModulePermission('hrm_project')"
            class="app-sidebar__heading"
          >
            Project Related
            <br />
          </li>
          
          <li
            v-if="hasModelPermission('client')"
            :class="{
              'mm-active': currentRoutePath(['/add-client', '/client-list']),
            }"
          >
            <a @click="OpenMenu($event)">
              <i class="metismenu-icon pe-7s-user"></i>
              Client
              <i class="metismenu-state-icon pe-7s-angle-down caret-left"></i>
            </a>
            <ul
              class="mm-collapse"
              :class="{
                'mm-show': currentRoutePath(['/add-client', '/client-list']),
              }"
            >
              <li v-if="hasPermission('add_client')">
                <router-link
                  :to="{ path: '/add-client' }"
                  :class="{ 'mm-active': currentRoutePath(['/add-client']) }"
                  >Add Client</router-link
                >
              </li>
              <li v-if="hasPermission('view_client')">
                <router-link
                  :to="{ path: '/client-list' }"
                  :class="{ 'mm-active': currentRoutePath(['/client-list']) }"
                  >Client list</router-link
                >
              </li>
            </ul>
          </li>

          
          <li
            v-if="hasModelPermission('project')"
            :class="{
              'mm-active': currentRoutePath([
                '/add-new-project',
                '/project-list',
              ]),
            }"
          >
            <a @click="OpenMenu($event)">
              <i class="metismenu-icon pe-7s-drawer"></i>
              Projects
              <i class="metismenu-state-icon pe-7s-angle-down caret-left"></i>
            </a>
            <ul
              class="mm-collapse"
              :class="{
                'mm-show': currentRoutePath([
                  '/add-new-project',
                  '/project-list',
                ]),
              }"
            >
              <li v-if="hasPermission('add_project')">
                <router-link
                  :to="{ path: '/add-new-project' }"
                  :class="{
                    'mm-active': currentRoutePath(['/add-new-project']),
                  }"
                  >Add New Project</router-link
                >
              </li>
              <li v-if="hasPermission('view_project')">
                <router-link
                  :to="{ path: '/project-list' }"
                  :class="{ 'mm-active': currentRoutePath(['/project-list']) }"
                  >Project list</router-link
                >
              </li>
            
            </ul>
          </li>
          
          <li
            v-if="
              hasPermission('view_worktype') ||
              hasPermission('view_workstatus') ||
              hasPermission('view_workpriority')
            "
            :class="{
              'mm-active': currentRoutePath([
                '/work-type',
                '/work-status',
                '/work-priority',
              ]),
            }"
          >
            <a @click="OpenMenu($event)">
              <i class="metismenu-icon pe-7s-drawer"></i>
              All Category
              <i class="metismenu-state-icon pe-7s-angle-down caret-left"></i>
            </a>
            <ul
              class="mm-collapse"
              :class="{
                'mm-show': currentRoutePath([
                  '/work-type',
                  '/work-status',
                  '/work-priority',
                ]),
              }"
            >
              
              <li v-if="hasPermission('view_worktype')">
                <router-link
                  :to="{ path: '/work-type' }"
                  :class="{ 'mm-active': currentRoutePath(['/work-type']) }"
                  >Work Type</router-link
                >
              </li>

              
              <li v-if="hasPermission('view_workstatus')">
                <router-link
                  :to="{ path: '/work-status' }"
                  :class="{ 'mm-active': currentRoutePath(['/work-status']) }"
                  >Work Status</router-link
                >
              </li>
              
              <li v-if="hasPermission('view_workpriority')">
                <router-link
                  :to="{ path: '/work-priority' }"
                  :class="{ 'mm-active': currentRoutePath(['/work-priority']) }"
                  >Work Priority</router-link
                >
              </li>
            </ul>
          </li>
        </ul> -->
          <!--Project End-->
          <!-- notice start -->
          <ul class="vertical-nav-menu mt-0">
            <li
              class="app-sidebar__heading"
              v-if="hasModulePermission('hrm_notice')"
            >
              {{ $store.getters.GET_NOTICE }}
              <br />
            </li>
            <!-- Notice -->
            <li
              v-if="hasModelPermission('notice')"
              :class="{
                'mm-active': currentRoutePath([
                  '/add-new-notice',
                  '/all-notices',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="currentRoutePath(['/add-new-notice', '/all-notices'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-bell"></i>
                    {{ $store.getters.GET_NOTICE }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_notice')">
                    <router-link
                      :to="{ path: '/add-new-notice' }"
                      :class="{
                        'mm-active': currentRoutePath(['/add-new-notice']),
                      }"
                      >{{ $store.getters.GET_CREATE }}</router-link
                    >
                  </li>
                  <li v-if="hasPermission('view_notice')">
                    <router-link
                      :to="{ path: '/all-notices' }"
                      :class="{
                        'mm-active': currentRoutePath(['/all-notices']),
                      }"
                      >{{ $store.getters.GET_LIST }}</router-link
                    >
                  </li>
                </ul>
              </details>
            </li>
          </ul>
          <!--Notice End-->
          <!--Multilang Start  -->
          <ul class="vertical-nav-menu mt-0">
            <li
              class="app-sidebar__heading"
              v-if="hasModulePermission('hrm_language')"
            >
              {{ $store.getters.GET_MULTILANG }}
              <br />
            </li>
            <li
              v-if="hasModelPermission('language')"
              :class="{
                'mm-active': currentRoutePath([
                  '/add-new-language',
                  '/all-languages',
                ]),
              }"
            >
              <!-- @click="colseOther($event)" -->
              <details
                class="dropdown"
                :open="
                  currentRoutePath(['/add-new-language', '/all-languages'])
                "
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-global"></i>
                    {{ $store.getters.GET_LANGUAGE }}
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('add_language')">
                    <router-link
                      :to="{ path: '/add-new-language' }"
                      :class="{
                        'mm-active': currentRoutePath(['/add-new-language']),
                      }"
                      >{{ $store.getters.GET_CREATE }}
                    </router-link>
                  </li>
                  <li v-if="hasPermission('view_language')">
                    <router-link
                      :to="{ path: '/all-languages' }"
                      :class="{
                        'mm-active': currentRoutePath(['/all-languages']),
                      }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
                <!--Multilang End-->
              </details>
            </li>
          </ul>
          <!-- multilang end -->
          <!--File Start  -->
          <ul class="vertical-nav-menu">
            <li
              class="app-sidebar__heading"
              v-if="hasModulePermission('hrm_file')"
            >
              File
              <br />
            </li>

            <li
              v-if="hasModelPermission('file')"
              :class="{
                'mm-active': currentRoutePath(['/file-list']),
              }"
            >
              <details
                class="dropdown"
                :open="currentRoutePath(['/file-list'])"
              >
                <summary>
                  <span>
                    <i class="metismenu-icon pe-7s-file"></i>
                    File List
                    <i
                      class="metismenu-state-icon pe-7s-angle-down caret-left"
                    ></i>
                  </span>
                </summary>
                <ul>
                  <li v-if="hasPermission('view_file')">
                    <router-link
                      :to="{ path: '/file-list' }"
                      :class="{ 'mm-active': currentRoutePath(['/file-list']) }"
                      >{{ $store.getters.GET_LIST }}
                    </router-link>
                  </li>
                </ul>
              </details>
            </li>
            <!--  -->
          </ul>
          <!-- file end -->
          <ul class="vertical-nav-menu">
            <li
              class="app-sidebar__heading"
              v-if="
                hasModulePermission('hrm_voice') &&
                hasModelPermission('voiceeventdata') &&
                hasPermission('add_voiceeventdata') &&
                hasPermission('change_voiceeventdata') &&
                hasPermission('delete_voiceeventdata') &&
                hasPermission('view_voiceeventdata')
              "
            >
              Voice
              <br />
            </li>
            <!-- v-if="hasModelPermission('file')" -->
            <li
              v-if="
                hasModelPermission('voiceeventdata') &&
                hasPermission('add_voiceeventdata') &&
                hasPermission('change_voiceeventdata') &&
                hasPermission('delete_voiceeventdata') &&
                hasPermission('view_voiceeventdata')
              "
            >
              <router-link
                :to="{ path: '/voice-configuration' }"
                :class="{
                  'mm-active': currentRoutePath(['/voice-configuration']),
                }"
              >
                <i class="metismenu-icon pe-7s-tools"></i>
                Voice Configuration
              </router-link>
            </li>
            <!--  -->
          </ul>
          <!-- file end -->
        </nav>
      </div>
    </div>
    <!--Sidebar Menu End-->
  </div>
</template>

<script>
import permissions from "@/authorization/permissions";
import "../../../assets/scripts/main";
// import $ from "jquery";

export default {
  name: "Sidebar",
  data() {
    return {};
  }, // data

  methods: {
    colseOther(event) {
      // var nav = document.querySelector(".vertical-nav-menu");
      // if (!event.target.open) return;
      // // Get all other open dropdowns and close them
      // var dropdowns = nav.querySelectorAll(".dropdown[open]");
      // Array.prototype.forEach.call(dropdowns, function (dropdown) {
      //   if (dropdown === event.target) return;
      //   dropdown.removeAttribute("open");
      // });
      console.log("kjkjkj", event);
      let removeAnchors = [...document.querySelectorAll("details")];
      removeAnchors.forEach((removeAnchor) => {
        removeAnchor.removeAttribute("open");
      });
      // e.target.nextSibling.removeAttribute("open");
      event.target.setAttribute("open", "");
    },
    new_method() {
      var nav = document.querySelector(".my-nav");
      nav.addEventListener(
        "toggle",
        function (event) {
          // Only run if the dropdown is open
          if (!event.target.open) return;
          // Get all other open dropdowns and close them
          var dropdowns = nav.querySelectorAll(".dropdown[open]");
          Array.prototype.forEach.call(dropdowns, function (dropdown) {
            if (dropdown === event.target) return;
            dropdown.removeAttribute("open");
          });
        },
        true
      );
    },
    currentRoutePath(routeName) {
      return routeName.includes(this.$route.path);
    },
    hasModulePermission(...module_name) {
      return permissions.hasModulePermission(...module_name);
      // return permissions.hasModulePermission.apply(...module_name)
    },

    hasModelPermission(model_name) {
      return permissions.hasModelPermission(model_name);
    },

    hasPermission(permission_name) {
      return permissions.hasPermission(permission_name);
    },
    OpenMenu(e) {
      let accordionItems = [...document.getElementsByClassName("mm-collapse")];
      accordionItems.forEach((accordionItem) => {
        accordionItem.classList.remove("mm-show");
      });
      let liItems = [...document.querySelectorAll("li")];
      liItems.forEach((liItem) => {
        liItem.classList.remove("mm-active");
      });
      let removeAnchors = [...document.querySelectorAll("a")];
      removeAnchors.forEach((removeAnchor) => {
        removeAnchor.classList.remove("mm-active");
      });
      e.target.nextSibling.classList.add("mm-show");
      // console.log(".", e.target.nextSibling.classList.add("mm-show"));
    },

    // opren menu back
    // OpenMenu(e) {
    //   let accordionItems = [...document.getElementsByClassName("mm-collapse")];
    //   accordionItems.forEach((accordionItem) => {
    //     accordionItem.classList.remove("mm-show");
    //   });
    //   let liItems = [...document.querySelectorAll("li")];
    //   liItems.forEach((liItem) => {
    //     liItem.classList.remove("mm-active");
    //   });
    //   let removeAnchors = [...document.querySelectorAll("a")];
    //   removeAnchors.forEach((removeAnchor) => {
    //     removeAnchor.classList.remove("mm-active");
    //   });

    //   console.log(".", e.target.nextSibling.classList.add("mm-show"));
    // },
  }, // methods

  created() {}, // created
}; // export default
// $(document).ready(function () {
//   $("#nav-mobile ul").hide();
//   $("#nav-mobile a").click(function (e) {
//     e.preventDefault();
//     var $menuItem = $(this).next("ul");
//     $menuItem.slideToggle();
//     $("#nav-mobile ul").not($menuItem).slideUp();
//   });
// });
</script>

<style scoped>
/* @import "../../main.css"; */
/* side bar scroll */
.app-sidebar__heading {
  color: #6e768e;
}
.vertical-nav-menu ul > li > a.mm-active {
  color: #57c5a5;
}
.vertical-nav-menu li.mm-active > a {
  color: #57c5a5;
}
.vertical-nav-menu li a.mm-active {
  color: #57c5a5;
  background: #57c5a51f;
}

/*  scroll sidebar */
.app-sidebar .app-sidebar__inner {
  padding: 2px 1.5rem 1.5rem;
  position: absolute;
  width: 279px;
  font-size: 13px;
  overflow-y: scroll;
  top: 0;
  bottom: 0;
  margin-top: 5px;
}
/* style  scrollbar*/
/* width */
::-webkit-scrollbar {
  width: 6px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: none;
  border-radius: 10px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgba(0, 0, 0, 0.1);
}

/*  a active  bg color */

.app-header__logo .logo-src {
  height: 23px;
  width: 97px;
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGEAAAAXCAYAAAAbfSF/AAAGKklEQVRoQ+2ZeVDUZRjHvwssoECbgHIJbMS6ILkcglJJKWo6Xohm5R8dU1ONf5g2kyllajEZWmNaUzY2zTTNNKVjkHiiphJmIIjLJfd97i6HsLuwywI2zyu77tKy4G93hprZ98/fvu/ze97n85y/5W356+d7sK8ptQDPDmFK7c9ebocw9QzsEP4DDOwQ/hcQ3PkuWBsUiUjP2Zju5IwerRo3FQ3Iai3D0MgIu0OsdzBen/O0yX3UQ1q0qHtwqrEIDaou9tsjfFekxW1AesNtXG4rf+j7vxIaj7iZQuzKzwDJN15jddCNDEOhUSJXXo8r7RUYufeg/9j8+AIk+ISy5yfrC83qsS4oEitnR7C7/lh9g+3RP9uWexwkX3+fql4ZDpf9YSKH7+CII/Ev4kJLGTKbiize1WJNcHXk433JCkxz5ON8SynuDg4gxMMbiX5hqOztwDfl10wg/FqXD/mAkj0jeIv9xBC6e+FQ6SXUKTutguDs4IS0uGSQTvSePzuqzULQ60BGEAlmYbGvGFV9Mnxbfs0AQg9BqdMgpSDDBBArlABS5yfB08VtUhDozA9V13Grs8mgk80gbBBGY6l/GPZLz6O1/67hBeRFdBGiT16g98IDxRfQqOo27HNxdEJqTBJqlHIcq8ixCsKCmUK8KnoStX0KOPAc8EXJRbMQxuoQ7RWIN8UJJtFHukd7BsKN74LvKrJR0t1qIkss8MG2iKXo02lQcbdjwkigqFDptPj49hkMjgwxWTaD8FlsMprVPcyLjBeFIUXIueZS3JDXjguBzrwTkQgPvis+lZ6zCsLWuYlw5PGQI6vGG3MWYW9hJhQalUGt8RyBNrw37zkWmfsKT7P9BCHUYyb6dAPoH9Lh+8ock/sRbJ9pj7AI6dSoJoRAqXWRTyiutVcZUo9NIDg7OuHwwheQ1XoHpxqlFnPaeAagsN4XsxZdWjW+KrvCGYLAeRr2x67H8boC5Crq8XncRlxsvYOzzSWTgrBRGMMiWp/LCUK4wBenm4rxsigeKfnpUA8NMlkUvQdiN+C3hkIs8hWhvb93QghU4/Q1I1V6hjmHTSCQ5xyM28gAEAhLSw+BUgRFDi03Jxcs8w9Don8YuwQVOK6FeXnAXKwPjkRKfgZLEW+HPQO/6QKDZ9P7LEXCMv9wUGrdlZ/OzhMEyYwA7CnMRFpsMjKbipHdUcX0jp8Vgs0hcWzvDskKNKm6JwXhanslPoxaBcWAEkcrsqcOwlhQmmEdC08KU1pcIeyOWsU89cvSy0wO1YfXRE/hYEkWGpT3O6+HhRDjFYQdN0/ipZA4BLt74kBxFpOzPWIpa0DIcVJj1qFW2TkpCJSSwh/1w9a5S1jDQrXS6u6ISzr6qSYXsoE+dhm1TotOrcqk8+ACIdDNEymRKxnM67IaJps6pH3Ra1l9oBQ1EQR9Otqee4IVToqEBd5CvJt3AsHuXtgpWYFPWFEdZl3RkdGGg1JgVa980hBID32UphVdwKGFm6xvUS0V5o+iVyOzsQg5shqLXmgcHVwgbHpsPpb4ic1mQ+pIdhWkM9ATFWYPvgv2GhXmhd5CbM87weRSpJX2tGFweIilIyr6NFVwgeDl6o49UatZzVodOM96CORBif7if7eoviKWN6kGUP9vyQDWQHDg8UCOQNFFnZjxohSSFByFo+XZKOlpHVcHGjLJOzMapbg0WtsoEowhUN2i+qUbGUGevA7nWu6/iwsEOrcmUILlAeGsLlg9rNGQtlOyknUMY4e1ou4WNqBMlArMQcjpqMatrgeDDe3RDg+hcXSy1p+ZNyMAW8KfxbHKHEi7mk0gOPEcsD82GZW9MqaH3hF+qb0JmUYJ+l0k8EGinxg1fXKWp/VT81gI1IQQbIK++9Yp9Gj7rYJAxt8bvYYNe1ZDIE1IwaSgSEhGP1t0adT4W16LS23lhks9bCSYyy3UCqZKz5r8RPPAHMEsfFDwO4bv3f9EYryeF8YgwVeEnfnpeGKGv8mnE/qkItf0IU9RjyttlSbnx0IgmW+JE5izfX3nquEVXCOBBOiHRJtAMJuM7Q9tagH7/wk2NSc3YXYI3Oxm01N2CDY1Jzdhdgjc7GbTU3YINjUnN2H/AL69QTIQo7CnAAAAAElFTkSuQmCC);
  margin-left: 45px;
  opacity: 1;
}

/* demo Test menu CSS */

/* .my-nav {
  list-style: none;
  margin-left: -0.5em;
  margin-right: -0.5em;
  padding: 0;
}

.my-nav > li {
  display: block;
  margin-left: 0.5em;
  margin-right: 0.5em;
} */

@media (min-width: 40em) {
  .my-nav > li {
    display: inline-block;
  }
}

/**
 * @bugfix Prevent webkit from removing list semantics
 * 1. Add a non-breaking space
 * 2. Make sure it doesn't mess up the DOM flow
 */
/* .my-nav > li:before {
  content: "\200B"; 
  position: absolute; 
} */

/**
 * Style the clickable text
 * Add your own styles to match other navigation items
 */
.dropdown > summary {
  cursor: pointer;
  /* Customize from here down */
  /* color: blue; */
}

/**
 * Position the dropdown content
 */
/* .dropdown {
  display: inline-block;
  position: relative;
} */

/**
 * Style the dropdown list
 */
/* .dropdown > ul {
  background-color: #ffffff;
  border-radius: 0.25em;
  list-style: none;
  margin: 0;
  padding: 0;
  min-width: 19em;
  position: absolute;
  top: 1.5em;
  z-index: 999;
} */

/**
 * @bugfix Prevent webkit from removing list semantics
 * 1. Add a non-breaking space
 * 2. Make sure it doesn't mess up the DOM flow
 */
/* .dropdown > ul > li:before {
  content: "\200B"; 
  position: absolute; 
} */
/*  */
.CursorPointer {
  cursor: pointer;
}

/* HIDE SUMMERY MARKER */
details > summary {
  list-style: none;
}
details > summary::-webkit-details-marker {
  display: none;
}
/* VERTICAL NAV SPAN */
.vertical-nav-menu li summary span {
  display: block;
  line-height: 2.4rem;
  height: 2.4rem;
  padding: 0 1.5rem 0 45px;
  position: relative;
  border-radius: 0.25rem;
  color: #343a40;
  white-space: nowrap;
  transition: all 0.2s;
  margin: 0.1rem 0;
}

.vertical-nav-menu li.mm-active > details summary span {
  color: #57c5a5;
}

.vertical-nav-menu li.mm-active > details summary span {
  font-weight: bold;
}
/* hover */
.vertical-nav-menu li summary span:hover {
  background: #57c5a51f;
  text-decoration: none;
  /* color: red; */
}
</style>
