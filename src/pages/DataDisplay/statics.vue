<template>
  <div>
    <div class="gap-8 m-5 grid grid-cols-2 mt-30">
      <n-card v-for="obj in staticsData" v-bind:key='obj'>
        <div class="font-bold">{{ obj.serial_num }}. {{ obj.question }}</div>
        <div v-for="opt in obj.options" class="m-6">
          <div class="relative border rounded">
            <div class="inline absolute left-0 rounded bg-cyan-400 h-full opacity-15" :style="{width: 100*opt.count/totalNum+'%'}"></div>
            <span class="ml-4">{{ opt.content }}</span>
            <span class="absolute right-60 font-bold">{{ opt.count }}</span>
            <span class="absolute right-4">{{ (opt.count/totalNum*100).toFixed(2) }}%</span>
          </div>
        </div>
      </n-card>
    </div>
    <el-pagination
      :current-page="pageNum"
      layout="prev, pager, next"
      :page-count="totalPageNum"
      @current-change="handleCurrentChange"
    />
  </div>
</template>

<script setup lang="ts">
import { useRequest } from 'vue-hooks-plus';
import { getStaticsDataAPI } from '@/apis';
import { useMainStore } from '@/stores';
import {ElNotification, ElPagination} from 'element-plus';
import { ref } from 'vue';
import { NCard } from 'naive-ui';

const tempStore = useMainStore().useTempStore();
const pageNum = ref(1);
const pageSize = 8;
const totalPageNum = ref();
const totalNum = ref();
const staticsData = ref();

const handleCurrentChange = (val: number) => {
  pageNum.value = val;
  getAnswers();
}

const getAnswers = () => {
  useRequest(() => getStaticsDataAPI({
    id: tempStore.checkId,
    page_num: pageNum.value,
    page_size: pageSize,
  }), {
    onSuccess(res: any) {
      res = tttdata;
      if(res.code === 200) {
        staticsData.value = res.data.statistics;
        totalNum.value = res.data.total;
        totalPageNum.value = res.data.total_sum_page;
      }
    },
    onError(e: any) {
      ElNotification.error('获取失败，请重试' + e);
    }
  })
}
getAnswers();

const tttdata = {
    "code": 200,
    "data": {
        "statistics": [
            {
                "serial_num": 3,
                "question": "性别",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "男",
                        "count": 122
                    },
                    {
                        "serial_num": 2,
                        "content": "女",
                        "count": 65
                    }
                ]
            },
            {
                "serial_num": 4,
                "question": "所在校区",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "朝晖校区",
                        "count": 181
                    },
                    {
                        "serial_num": 2,
                        "content": "屏峰校区",
                        "count": 6
                    }
                ]
            },
            {
                "serial_num": 5,
                "question": "学院",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "化学工程学院",
                        "count": 15
                    },
                    {
                        "serial_num": 2,
                        "content": "生物工程学院",
                        "count": 3
                    },
                    {
                        "serial_num": 3,
                        "content": "药学院、绿色制药协同创新中心",
                        "count": 6
                    },
                    {
                        "serial_num": 4,
                        "content": "环境学院",
                        "count": 4
                    },
                    {
                        "serial_num": 5,
                        "content": "材料科学与工程学院",
                        "count": 7
                    },
                    {
                        "serial_num": 6,
                        "content": "食品科学与工程学院",
                        "count": 3
                    },
                    {
                        "serial_num": 7,
                        "content": "机械工程学院",
                        "count": 11
                    },
                    {
                        "serial_num": 8,
                        "content": "信息工程学院",
                        "count": 12
                    },
                    {
                        "serial_num": 9,
                        "content": "计算机科学与技术学院",
                        "count": 59
                    },
                    {
                        "serial_num": 10,
                        "content": "土木工程学院",
                        "count": 10
                    },
                    {
                        "serial_num": 12,
                        "content": "物理学院",
                        "count": 1
                    },
                    {
                        "serial_num": 13,
                        "content": "数学科学学院",
                        "count": 3
                    },
                    {
                        "serial_num": 14,
                        "content": "管理学院",
                        "count": 7
                    },
                    {
                        "serial_num": 15,
                        "content": "经济学院",
                        "count": 4
                    },
                    {
                        "serial_num": 16,
                        "content": "教育学院",
                        "count": 7
                    },
                    {
                        "serial_num": 17,
                        "content": "外国语学院",
                        "count": 3
                    },
                    {
                        "serial_num": 18,
                        "content": "人文学院",
                        "count": 8
                    },
                    {
                        "serial_num": 19,
                        "content": "设计与建筑学院",
                        "count": 5
                    },
                    {
                        "serial_num": 20,
                        "content": "法学院",
                        "count": 2
                    },
                    {
                        "serial_num": 21,
                        "content": "公共管理学院",
                        "count": 1
                    },
                    {
                        "serial_num": 22,
                        "content": "健行学院",
                        "count": 16
                    }
                ]
            },
            {
                "serial_num": 9,
                "question": "第一志愿",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "常务处",
                        "count": 35
                    },
                    {
                        "serial_num": 2,
                        "content": "小弘工作室",
                        "count": 20
                    },
                    {
                        "serial_num": 3,
                        "content": "产研部——技术",
                        "count": 83
                    },
                    {
                        "serial_num": 4,
                        "content": "产研部——产品",
                        "count": 28
                    },
                    {
                        "serial_num": 5,
                        "content": "编辑工作室",
                        "count": 2
                    },
                    {
                        "serial_num": 6,
                        "content": "视觉影像部",
                        "count": 19
                    }
                ]
            },
            {
                "serial_num": 10,
                "question": "第二志愿",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "常务处",
                        "count": 27
                    },
                    {
                        "serial_num": 2,
                        "content": "小弘工作室",
                        "count": 34
                    },
                    {
                        "serial_num": 3,
                        "content": "产研部——技术",
                        "count": 42
                    },
                    {
                        "serial_num": 4,
                        "content": "产研部——产品",
                        "count": 49
                    },
                    {
                        "serial_num": 5,
                        "content": "编辑工作室",
                        "count": 18
                    },
                    {
                        "serial_num": 6,
                        "content": "视觉影像部",
                        "count": 17
                    }
                ]
            },
            {
                "serial_num": 13,
                "question": "是否服从调剂",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "是",
                        "count": 132
                    },
                    {
                        "serial_num": 2,
                        "content": "否",
                        "count": 55
                    }
                ]
            },
            {
                "serial_num": 14,
                "question": "请确认",
                "question_type": 1,
                "options": [
                    {
                        "serial_num": 1,
                        "content": "精弘网络，启动！",
                        "count": 187
                    }
                ]
            }
        ],
        "total": 187,
        "total_sum_page": 1
    },
    "msg": "OK"
}

</script>