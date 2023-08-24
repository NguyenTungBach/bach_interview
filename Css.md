# 1. Cột trong bảng muốn để nằm ngang, không dọc
VD cột lỗi:
- VD đoạn code lỗi
```sh
<b-th
    class="th-sort th-name th-course-name"
    :colspan="3"
    @click="onSortTable('total_payable')"
>
    <b-row>
        <b-col>
            {{ $t('LIST_CASH.TABLE_CASH_DISBURSEMENT_TOTAL_ACCOUNTS_RECEIVABLE') }}
        </b-col>
        <b-col class="icon-sorts">
            <div class="text-right">
                <i
                    v-if="sortTable.sortBy === 'total_payable' && sortTable.sortType === true"
                    class="fad fa-sort-up icon-sort"
                />
                <i
                    v-else-if="sortTable.sortBy === 'total_payable' && sortTable.sortType === false"
                    class="fad fa-sort-down icon-sort"
                />
                <i
                    v-else
                    class="fa-solid fa-sort icon-sort-default"
                />
            </div>
        </b-col>
    </b-row>
</b-th>
```

![](https://res.cloudinary.com/dark-faith/image/upload/v1692862955/css-veho/col_need_fix.png)

### 1.1 Fix lỗi trên
VD từng cột th: (chú ý thẻ [div, span], class: [th-sort, icon-sorts, th-col]) thứ tự dưới đây
- th-sort (class th-sort)
    - div (class: th-col)
       - span 
       - div (class boostrap: icon-sorts, text-right)
```sh
<b-th
    class="th-sort th-id th-course-id"
    :rowspan="2"
    @click="onSortTable('customer_code')"
>
    <div class="row-cashCiept-id th-col">
        <span>
            {{ $t('LIST_CASH.TABLE_CASH_ID') }}
        </span>
        <div class="icon-sorts text-right">
            <i
                v-if="sortTable.sortBy === 'customer_code' && sortTable.sortType === true"
                class="fad fa-sort-up icon-sort"
            />
            <i
                v-else-if="sortTable.sortBy === 'customer_code' && sortTable.sortType === false"
                class="fad fa-sort-down icon-sort"
            />
            <i
                v-else
                class="fa-solid fa-sort icon-sort-default"
            />
        </div>
    </div>
</b-th>
```

đoạn css như sau:
```sh
.th-col {
    display: flex;
    align-items: center;
    justify-content: space-between;

    span {
        white-space: nowrap;
    }
}

th.th-sort {
    cursor: pointer;

    .icon-sorts {
        margin-left: 15px;

        i.icon-sort-default {
            color: $white;
            opacity: 0.7;
        }
    }
}
```

VD cột sau khi fix:

![](https://res.cloudinary.com/dark-faith/image/upload/v1692863046/css-veho/col_fixed.png)
