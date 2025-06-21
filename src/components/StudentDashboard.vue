<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'

// Reactive data
const currentTime = ref(new Date())
const user = ref({
  name: 'Alex Johnson',
  email: 'alex.johnson@university.edu',
  avatar: 'https://images.pexels.com/photos/614810/pexels-photo-614810.jpeg?auto=compress&cs=tinysrgb&w=150&h=150&dpr=2',
  studentId: 'STU-2024-001'
})

const notifications = ref([
  { id: 1, message: 'Assignment due in 2 hours', type: 'urgent', time: '2 hours' },
  { id: 2, message: 'New course material uploaded', type: 'info', time: '1 day' },
  { id: 3, message: 'Grade posted for Math Quiz', type: 'success', time: '2 days' }
])

const courses = ref([
  {
    id: 1,
    name: 'Computer Science Fundamentals',
    code: 'CS-101',
    progress: 78,
    instructor: 'Dr. Sarah Wilson',
    students: 124,
    lessons: 24,
    duration: '12 weeks',
    nextClass: 'Today 2:00 PM',
    assignments: 3,
    image: 'https://images.pexels.com/photos/574071/pexels-photo-574071.jpeg?auto=compress&cs=tinysrgb&w=400&h=250&dpr=2'
  },
  {
    id: 2,
    name: 'Digital Marketing Strategy',
    code: 'MKT-205',
    progress: 92,
    instructor: 'Prof. Michael Chen',
    students: 89,
    lessons: 18,
    duration: '10 weeks',
    nextClass: 'Tomorrow 10:00 AM',
    assignments: 1,
    image: 'https://images.pexels.com/photos/265087/pexels-photo-265087.jpeg?auto=compress&cs=tinysrgb&w=400&h=250&dpr=2'
  },
  {
    id: 3,
    name: 'Data Structures & Algorithms',
    code: 'CS-202',
    progress: 65,
    instructor: 'Dr. James Rodriguez',
    students: 156,
    lessons: 32,
    duration: '16 weeks',
    nextClass: 'Wed 3:00 PM',
    assignments: 5,
    image: 'https://images.pexels.com/photos/1181263/pexels-photo-1181263.jpeg?auto=compress&cs=tinysrgb&w=400&h=250&dpr=2'
  },
  {
    id: 4,
    name: 'User Experience Design',
    code: 'DES-301',
    progress: 85,
    instructor: 'Lisa Thompson',
    students: 67,
    lessons: 20,
    duration: '8 weeks',
    nextClass: 'Thu 1:00 PM',
    assignments: 2,
    image: 'https://images.pexels.com/photos/196644/pexels-photo-196644.jpeg?auto=compress&cs=tinysrgb&w=400&h=250&dpr=2'
  }
])

const assignments = ref([
  {
    id: 1,
    title: 'React Component Library',
    course: 'CS-101',
    dueDate: '2024-01-15',
    status: 'pending',
    priority: 'high',
    type: 'Project'
  },
  {
    id: 2,
    title: 'Marketing Campaign Analysis',
    course: 'MKT-205',
    dueDate: '2024-01-18',
    status: 'submitted',
    priority: 'medium',
    type: 'Essay'
  },
  {
    id: 3,
    title: 'Binary Tree Implementation',
    course: 'CS-202',
    dueDate: '2024-01-20',
    status: 'pending',
    priority: 'high',
    type: 'Coding'
  },
  {
    id: 4,
    title: 'User Journey Mapping',
    course: 'DES-301',
    dueDate: '2024-01-22',
    status: 'draft',
    priority: 'low',
    type: 'Design'
  }
])

const stats = ref({
  totalCourses: 4,
  completedAssignments: 12,
  averageGrade: 87.5,
  studyStreak: 15
})

const recentActivity = ref([
  { id: 1, action: 'Completed', item: 'JavaScript Basics Quiz', course: 'CS-101', time: '2 hours ago' },
  { id: 2, action: 'Submitted', item: 'Marketing Report', course: 'MKT-205', time: '1 day ago' },
  { id: 3, action: 'Started', item: 'Algorithm Analysis', course: 'CS-202', time: '2 days ago' }
])

// Computed properties
const urgentNotifications = computed(() => 
  notifications.value.filter(n => n.type === 'urgent').length
)

const upcomingAssignments = computed(() => 
  assignments.value.filter(a => a.status === 'pending').length
)

// Methods
const formatDate = (date: string) => {
  return new Date(date).toLocaleDateString('en-US', { 
    month: 'short', 
    day: 'numeric' 
  })
}

const getDaysUntilDue = (dueDate: string) => {
  const today = new Date()
  const due = new Date(dueDate)
  const diffTime = due.getTime() - today.getTime()
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24))
  return diffDays
}

// Lifecycle
onMounted(() => {
  setInterval(() => {
    currentTime.value = new Date()
  }, 60000)
})
</script>

<template>
  <div class="studentdashboard">
    <!-- Sidebar -->
    <aside class="sidebarsd">
      <div class="sidebar-headersd">
        <div class="logosd">
          <div class="logo-iconsd">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/>
              <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
            </svg>
          </div>
          <span class="logo-textsd">Ed-Centure</span>
        </div>
      </div>

      <nav class="sidebar-nav">
        <a href="#" class="nav-itemsd active">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="3" y="3" width="7" height="7"/>
            <rect x="14" y="3" width="7" height="7"/>
            <rect x="14" y="14" width="7" height="7"/>
            <rect x="3" y="14" width="7" height="7"/>
          </svg>
          <span>Dashboard</span>
        </a>
        <a href="#" class="nav-itemsd">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/>
            <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
          </svg>
          <span>Courses</span>
        </a>
        <a href="#" class="nav-itemsd">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
            <polyline points="14,2 14,8 20,8"/>
            <line x1="16" y1="13" x2="8" y2="13"/>
            <line x1="16" y1="17" x2="8" y2="17"/>
          </svg>
          <span>Assignments</span>
        </a>
        <a href="#" class="nav-itemsd">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
          </svg>
          <span>Grades</span>
        </a>
        <a href="#" class="nav-itemsd">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="3" y="4" width="18" height="18" rx="2" ry="2"/>
            <line x1="16" y1="2" x2="16" y2="6"/>
            <line x1="8" y1="2" x2="8" y2="6"/>
            <line x1="3" y1="10" x2="21" y2="10"/>
          </svg>
          <span>Calendar</span>
        </a>
        <a href="#" class="nav-itemsd">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
          </svg>
          <span>Messages</span>
        </a>
      </nav>

      <div class="sidebar-footer">
        <div class="user-profilesd">
          <img :src="user.avatar" :alt="user.name" class="user-avatar" />
          <div class="user-info">
            <span class="user-name">{{ user.name }}</span>
            <span class="user-role">Student</span>
          </div>
        </div>
      </div>
    </aside>

    <!-- Main Content -->
    <main class="main-contentsd">
      <!-- Header -->
      <header class="headersd">
        <div class="header-leftsd">
          <h1 class="page-titlesd">Dashboard</h1>
          <p class="page-subtitlesd">Welcome back, {{ user.name.split(' ')[0] }}! Here's what's happening with your courses.</p>
        </div>
        
        <div class="header-rightsd">
          <div class="search-boxsd">
            <svg class="search-iconsd" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="11" cy="11" r="8"/>
              <path d="M21 21l-4.35-4.35"/>
            </svg>
            <input type="text" placeholder="Search courses, assignments..." />
          </div>
          
          <div class="notification-bellsd" :class="{ 'has-notificationssd': urgentNotifications > 0 }">
            <svg class="bell-iconsd" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/>
              <path d="M13.73 21a2 2 0 0 1-3.46 0"/>
            </svg>
            <span v-if="urgentNotifications > 0" class="notification-badgesd">{{ urgentNotifications }}</span>
          </div>
        </div>
      </header>

      <!-- Stats Cards -->
      <section class="stats-sectionsd">
        <div class="stats-gridsd">
          <div class="stat-card primarysd">
            <div class="stat-contentsd">
              <div class="stat-headersd">
                <span class="stat-labelsd">Total Courses</span>
                <div class="stat-iconsd">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/>
                    <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
                  </svg>
                </div>
              </div>
              <span class="stat-numbersd">{{ stats.totalCourses }}</span>
              <span class="stat-change positivesd">+2 from last semester</span>
            </div>
          </div>
          
          <div class="stat-cardsd">
            <div class="stat-contentsd">
              <div class="stat-headersd">
                <span class="stat-labelsd">Completed</span>
                <div class="stat-iconsd">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polyline points="20,6 9,17 4,12"/>
                  </svg>
                </div>
              </div>
              <span class="stat-numbersd">{{ stats.completedAssignments }}</span>
              <span class="stat-change positivesd">+3 this week</span>
            </div>
          </div>
          
          <div class="stat-cardsd">
            <div class="stat-contentsd">
              <div class="stat-headersd">
                <span class="stat-labelsd">Average Grade</span>
                <div class="stat-iconsd">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <circle cx="12" cy="12" r="10"/>
                    <polygon points="16.24,7.76 14.12,14.12 7.76,16.24 9.88,9.88 16.24,7.76"/>
                  </svg>
                </div>
              </div>
              <span class="stat-numbersd">{{ stats.averageGrade }}%</span>
              <span class="stat-change positivesd">+2.5% improvement</span>
            </div>
          </div>
          
          <div class="stat-cardsd">
            <div class="stat-contentsd">
              <div class="stat-headersd">
                <span class="stat-labelsd">Study Streak</span>
                <div class="stat-iconsd">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M8.5 14.5A2.5 2.5 0 0 0 11 12c0-1.38-.5-2-1-3-1.072-2.143-.224-4.054 2-6 .5 2.5 2 4.9 4 6.5 2 1.6 3 3.5 3 5.5a7 7 0 1 1-14 0c0-1.153.433-2.294 1-3a2.5 2.5 0 0 0 2.5 2.5z"/>
                  </svg>
                </div>
              </div>
              <span class="stat-numbersd">{{ stats.studyStreak }}</span>
              <span class="stat-changesd">days in a row</span>
            </div>
          </div>
        </div>
      </section>

      <!-- Main Grid -->
      <div class="content-gridsd">
        <!-- Courses Section -->
        <section class="courses-sectionsd">
          <div class="section-headersd">
            <h2 class="section-titlesd">My Courses</h2>
            <button class="view-all-btnsd">View All</button>
          </div>
          
          <div class="courses-gridsd">
            <div 
              v-for="course in courses" 
              :key="course.id" 
              class="course-cardsd"
            >
              <div class="course-imagesd">
                <img :src="course.image" :alt="course.name" />
                <div class="course-overlaysd">
                  <button class="play-btnsd">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                      <polygon points="5,3 19,12 5,21"/>
                    </svg>
                  </button>
                </div>
              </div>
              
              <div class="course-contentsd">
                <div class="course-headersd">
                  <h3 class="course-namesd">{{ course.name }}</h3>
                  <span class="course-codesd">{{ course.code }}</span>
                </div>
                
                <p class="course-instructorsd">{{ course.instructor }}</p>
                
                <div class="course-statssd">
                  <div class="course-statsd">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                      <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
                      <circle cx="9" cy="7" r="4"/>
                      <path d="M23 21v-2a4 4 0 0 0-3-3.87"/>
                      <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
                    </svg>
                    <span>{{ course.students }}</span>
                  </div>
                  <div class="course-statsd">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                      <polygon points="23,7 16,12 23,17 23,7"/>
                      <rect x="1" y="5" width="15" height="14" rx="2" ry="2"/>
                    </svg>
                    <span>{{ course.lessons }} lessons</span>
                  </div>
                </div>
                
                <div class="course-progresssd">
                  <div class="progress-infosd">
                    <span class="progress-labelsd">Progress</span>
                    <span class="progress-percentsd">{{ course.progress }}%</span>
                  </div>
                  <div class="progress-barsd">
                    <div 
                      class="progress-fillsd" 
                      :style="{ width: course.progress + '%' }"
                    ></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Right Sidebar -->
        <aside class="right-sidebar">
          <!-- Upcoming Assignments -->
          <div class="widget">
            <div class="widget-header">
              <h3 class="widget-title">Upcoming Assignments</h3>
              <span class="assignment-count">{{ upcomingAssignments }} pending</span>
            </div>
            
            <div class="assignments-list">
              <div 
                v-for="assignment in assignments.slice(0, 4)" 
                :key="assignment.id" 
                class="assignment-item"
                :class="`status-${assignment.status} priority-${assignment.priority}`"
              >
                <div class="assignment-type">{{ assignment.type }}</div>
                <div class="assignment-content">
                  <h4 class="assignment-title">{{ assignment.title }}</h4>
                  <span class="assignment-course">{{ assignment.course }}</span>
                  <div class="assignment-meta">
                    <span class="due-date">Due {{ formatDate(assignment.dueDate) }}</span>
                    <span 
                      class="days-left"
                      :class="{ 'urgent': getDaysUntilDue(assignment.dueDate) <= 2 }"
                    >
                      {{ getDaysUntilDue(assignment.dueDate) }} days left
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Recent Activity -->
          <div class="widget">
            <div class="widget-header">
              <h3 class="widget-title">Recent Activity</h3>
            </div>
            
            <div class="activity-list">
              <div 
                v-for="activity in recentActivity" 
                :key="activity.id" 
                class="activity-item"
              >
                <div class="activity-icon">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polyline points="20,6 9,17 4,12"/>
                  </svg>
                </div>
                <div class="activity-content">
                  <p class="activity-text">
                    <span class="activity-action">{{ activity.action }}</span>
                    {{ activity.item }}
                  </p>
                  <div class="activity-meta">
                    <span class="activity-course">{{ activity.course }}</span>
                    <span class="activity-time">{{ activity.time }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Quick Actions -->
          <div class="widget">
            <div class="widget-header">
              <h3 class="widget-title">Quick Actions</h3>
            </div>
            
            <div class="quick-actions">
              <button class="quick-action-btn primary">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="12" y1="5" x2="12" y2="19"/>
                  <line x1="5" y1="12" x2="19" y2="12"/>
                </svg>
                <span>New Assignment</span>
              </button>
              <button class="quick-action-btn">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="4" width="18" height="18" rx="2" ry="2"/>
                  <line x1="16" y1="2" x2="16" y2="6"/>
                  <line x1="8" y1="2" x2="8" y2="6"/>
                  <line x1="3" y1="10" x2="21" y2="10"/>
                </svg>
                <span>Schedule Study</span>
              </button>
              <button class="quick-action-btn">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
                </svg>
                <span>Message Instructor</span>
              </button>
            </div>
          </div>
        </aside>
      </div>
    </main>
  </div>
</template>