<template>
    <div class="container">
        <h1 class="title">Qarz qaytarish</h1>
        <form @submit.prevent="saveData">
            <label class="label" for="loanSelect"
                >Qarz arizasi raqamini tanlang</label
            >
            <select class="option" id="loanSelect" v-model="selectedLoan">
                <label class="label" for="loan">Ma'lumotlar:</label>
                <option
                    id="loan"
                    v-for="(loan, index) in loans"
                    :key="index"
                    :value="loan"
                >
                    {{ loan.lender }}
                </option>
            </select>

            <table v-if="selectedLoan" class="table">
                <thead>
                    <tr class="tablehead">
                        <th class="th">Qarz beruvchi</th>
                        <th class="th">Olingan sana</th>
                        <th class="th">Qaytarish muhlati</th>
                        <th class="th">Pul miqdori</th>
                        <th class="th">Qoldiq</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="tablebody">
                        <td class="td">{{ selectedLoan.lender }}</td>
                        <td class="td">{{ selectedLoan.date }}</td>
                        <td class="td">{{ selectedLoan.repaymentPeriod }}</td>
                        <td class="td">
                            {{ selectedLoan.amount }} {{ selectedCurrency }}
                        </td>
                        <td class="td">
                            {{ selectedLoan.balance }} {{ selectedCurrency }}
                        </td>
                    </tr>
                </tbody>
            </table>

            <div class="money">
                <div class="miqdor">
                    <label class="label" for="moneyAmount">Pul miqdori</label>
                    <input
                        class="balans"
                        type="text"
                        id="moneyAmount"
                        :value="selectedLoan?.balance"
                        disabled
                    />
                </div>

                <div class="valyuta">
                    <label class="label" for="currency">Valyuta</label>
                    <select
                        class="height2"
                        id="currency"
                        v-model="selectedCurrency"
                    >
                        <option value="UZS">UZS</option>
                        <option value="USD">USD</option>
                        <option value="RUB">RUB</option>
                    </select>
                </div>
            </div>

            <div class="qaytarishwrap">
                <label class="label" for="returnDate">Qaytarish sanasi</label>
                <input
                    class="qaytarish"
                    id="returnDate"
                    :value="selectedLoan?.repaymentPeriod"
                    disabled
                />
            </div>

            <div class="buttons">
                <button class="button1" type="submit">Save</button>
                <button class="button2" type="button" @click="cancel">
                    Cancel
                </button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            loans: [
                {
                    lender: "1",
                    date: "09.10.2023",
                    repaymentPeriod: "28.11.2023",
                    amount: 10000,
                    balance: 5000,
                },
                {
                    lender: "2",
                    date: "02.09.2023",
                    repaymentPeriod: "05.10.2024",
                    amount: 30000,
                    balance: 6000,
                },
                {
                    lender: "3",
                    date: "31.12.2023",
                    repaymentPeriod: "25.06.2024",
                    amount: 20000,
                    balance: 7000,
                },
            ],
            selectedLoan: null,
            moneyAmount: null,
            selectedCurrency: "USD",
            returnDate: null,
        };
    },
    mounted() {
        this.selectedLoan = this.loans[0];
    },
    methods: {
        saveData() {
            console.log("Data saved!");
        },
        cancel() {
            this.selectedLoan = this.loans[0];
            this.moneyAmount = null;
            this.selectedCurrency = "UZS";
            this.returnDate = null;
        },
    },
};
</script>
<style>
.container {
    max-width: 50%;
    margin: 0 auto;
    border: 1px solid black;
    padding: 10px;
}
.title {
    text-align: center;
}
.option {
    width: 100%;
    height: 30px;
}
.table {
    display: grid;
    grid-template-columns: repeat(2, 50%);
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
}
.tablehead {
    display: flex;
    min-width: 50%;
    flex-direction: column;
}
.tablebody {
    min-width: 50%;
    display: flex;
    flex-direction: column;
}

.table-container {
    overflow-x: auto;
}

.th,
.td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}
.label {
    font-size: 19px;
}
.money {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: space-between;
}
.buttons {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.button1 {
    padding: 10px;
    color: white;
    background: green;
    border: none;
    outline: none;
    font-size: 17px;
    width: 150px;
}
.button2 {
    padding: 10px;
    color: white;
    background: red;
    border: none;
    outline: none;
    font-size: 17px;
    width: 150px;
}
.valyuta {
    display: flex;
    align-items: left;
    flex-direction: column;
    width: 49%;
}
.miqdor {
    display: flex;
    align-items: left;
    flex-direction: column;
    width: 49%;
}
.balans {
    height: 30px;
    border: 1px solid black;
    text-align: center;
}
.height2 {
    height: 32px;
    text-align: center;
}
.qaytarishwrap {
    margin: 20px 0;
}
.qaytarish {
    width: 100%;
    border: 1px solid black;
    height: 30px;
    text-align: center;
}
</style>
